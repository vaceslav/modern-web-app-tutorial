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


über swagger testen

## NSwag Studio <https://github.com/RSuter/NSwag/wiki/NSwagStudio>

swagger.ts generieren.

1. EntryComponent anpassen
1. EntriesService anpassen

testen!!

mit css spielen

Client über swagger generieren

implement delet