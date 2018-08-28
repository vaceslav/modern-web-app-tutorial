# LESSSON 4

## Code clonen

    dotnet restore

## Backend: .Net CORE Entity Framework

DB Erstellen

    ntt_time
    dotnet ef database update



Add TimeEntry.cs

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


in Context hinzufügen

    public DbSet<TimeEntry> TimeEntries { get; set; }

in console

    dotnet ef migrations add AddEntity
    dotnet ef database update



controlle rerstellen

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.EntityFrameworkCore;
    using NttTimeApi.Db;

    namespace ntt_time.Controllers
    {
        [Route("api/[controller]")]
        [ApiController]
        public class TimeEntryController : ControllerBase
        {

            private readonly NttDbContext _context;

            public TimeEntryController(NttDbContext context)
            {
                _context = context;
            }


            // GET api/values
            [HttpGet]
            [ProducesResponseType(typeof(List<TimeEntry>), 200)]
            public async Task<IActionResult> Get()
            {
                return Ok(await _context.TimeEntries.ToListAsync());
            }

            [HttpPost("")]
            [ProducesResponseType(typeof(TimeEntry), 200)]
            public async Task<IActionResult> Create([FromBody] TimeEntry entry)
            {
                var result = await _context.TimeEntries.AddAsync(entry);
                _context.SaveChanges();
                return Ok(entry);
            }

        }
    }

über swagger testen

## NSwag Studio <https://github.com/RSuter/NSwag/wiki/NSwagStudio>

swagger.ts generieren.

1. EntryComponent anpassen
1. EntriesService anpassen

testen!!

mit css spielen

Client über swagger generieren

implement delet