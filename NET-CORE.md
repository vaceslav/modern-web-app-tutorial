# .NET Core 2.1

    dotnet --version
    dotnet new
    dotnet new console --name testNetConsole

- open VS Code and directory

in project directory

    dotnet build
    dotnet run


go to bin/debug dir

    dotnet  {filename}.dll

in der console im Test-Verzeichnis

    dotnet new web --name testNetWeb

## CreateDefaultBuilder
- <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.1>

- <https://github.com/aspnet/MetaPackages/blob/release/2.1/src/Microsoft.AspNetCore/WebHost.cs#L133>

Webseite starten

    dotnet run

## Weitere Beispiele

    dotnet new angular --no-https --name testNetAngular
    dotnet new mvc --no-https --name testNetMvc

## WEB API Project

    dotnet new webapi --no-https --name testNetApi
    dotnet run
    dotnet watch run

publish

    dotnet publish --output app_dist --configuration Release
    cd app_dist
    dotnet .\testNetApi.dll


publish with runtime

    dotnet publish --output app_dist --configuration Release --runtime win-x64 --self-contained


## Middleware

create test.txt file in wwwroot

    app.UseStaticFiles();

swagger <https://swagger.io/>  
NSwag <https://github.com/RSuter/NSwag>  
NSwag Getting Started: <https://docs.microsoft.com/en-us/aspnet/core/tutorials/getting-started-with-nswag?view=aspnetcore-2.1&tabs=netcore-cli%2Cvisual-studio-xml>

    dotnet add package NSwag.AspNetCore

in ConfigureServices function

    services.AddSwagger();

in Configure function

     app.UseSwaggerUi3WithApiExplorer(s =>
            {
                s.SwaggerRoute = "/swagger/v1/swagger.json";
                s.SwaggerUiRoute = "/swagger";

                s.GeneratorSettings.DocumentProcessors.Add(new SecurityDefinitionAppender("TEST_HEADER", new SwaggerSecurityScheme
                {
                    Type = SwaggerSecuritySchemeType.ApiKey,
                    Name = "TEST_HEADER",
                    In = SwaggerSecurityApiKeyLocation.Header,
                    Description = "TEST_HEADER"
                }));
            });

## Entity Framework

- create Test DB: TestNtt

Pakete installieren

    dotnet add package Microsoft.EntityFrameworkCore.SqlServer
    dotnet add package Microsoft.EntityFrameworkCore.Design

Context erstellen

    using Microsoft.EntityFrameworkCore;

    namespace TestNttApi.Db {
    
    public class NttDbContext : DbContext
    {
        public NttDbContext(DbContextOptions<NttDbContext> options) : base(options)
        {
        }
    }
}


Configurieren

    var connection = @"Server=(localdb)\mssqllocaldb;Database=TestNtt;Trusted_Connection=True;ConnectRetryCount=0";";
     services.AddDbContext<NttDbContext>(options => options.UseSqlServer(connection));

Entity erstellen

    using System;

    public class TimeEntry
    {
        public TimeEntry()
        {
        }

        public int Id { get; set; }
        public DateTime Start { get; set; }

        public DateTime End { get; set; }
    }

## Migration

    dotnet ef migrations add InitialCreate
    dotnet ef database update

add time Entries

    public DbSet<TimeEntry> TimeEntries { get; set; }

create migration for time entries

    dotnet ef migrations add InitialCreate
    dotnet ef database update

controller für TimeEntry erstellen

    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.EntityFrameworkCore;
    using TestNttApi.Db;

    namespace Time.Controllers
    {

        [Route("api/[controller]")]    
        public class TimeEntryController : Controller
        {
            private readonly NttDbContext _context;
            public TimeEntryController(NttDbContext context)
            {
                _context = context;
            }

            [HttpGet("")]
            [ProducesResponseType( typeof( List<TimeEntry> ), 200 )]
            public async Task<IActionResult> Get()
            {
                return Ok(await _context.TimeEntries.ToListAsync());
            }

            [HttpPost("")]
            [ProducesResponseType( typeof(TimeEntry), 200 )]
            public async Task<IActionResult> Create([FromBody] TimeEntry entry)
            {
                var result = await _context.TimeEntries.AddAsync(entry);
                _context.SaveChanges();
                return Ok(entry);
            }
        }
    }