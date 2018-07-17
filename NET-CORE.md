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

publish

    dotnet publish --output app_dist --configuration Release
    cd app_dist
    dotnet .\testNetApi.dll


## Middleware

