# .NET Core + Angular 6.1

## Tools auf den aktuellen Stand bringen

    ng -v
    ---> 21.07.2018 -> 6.1.1 #wenn nicht 
    yarn global add @angular/cli
    dotnet --version 
    --> 2.1.301

## Git UI
1. SmartGit <https://www.syntevo.com/smartgit/>
1. Sourcetree <https://www.sourcetreeapp.com/>


## Time Projekt forken und clonen

    git clone xyz
    git clone https://github.com/vaceslav/ntt-time.git
    cd <in-to-dir>
    yarn
    dotnet restore

## VS Code Plugins

1. c#
1. Prettier -Code formatter
1. Sass
1. TSLint
1. vscode-icons

## [.NET Middleware](https://github.com/vaceslav/modern-web-app-tutorial/blob/master/NET-CORE.md#middleware)

    app.UseStaticFiles();
    dotnet add package NSwag.AspNetCore

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


## [.NET Entity Framework](https://github.com/vaceslav/modern-web-app-tutorial/blob/master/NET-CORE.md#entity-framework)


## Angular components

    ng g m shared
    ng g m time-view
    ng g c time-view/components/entry-list
    ng g c shared/components/entry --export

use shared module in time-view module

    imports: [
        CommonModule,
        SharedModule
    ],


Routing Module für Time-View erstellen

    ng g m time-view/time-view-routing --flat

Inhalt vom app-routing-module.ts kopieren.

    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { EntryListComponent } from './components/entry-list/entry-list.component';

    const routes: Routes = [
    {
        path: '',
        component: EntryListComponent
    }
    ];

    @NgModule({
    imports: [RouterModule.forChild(routes)],
    exports: [RouterModule]
    })
    export class TimeViewRoutingModule {}


TimeViewRouting in TimeViewBenutzen

    imports: [
        CommonModule, 
        SharedModule, 
        TimeViewRoutingModule
    ],

Lazy Loading für Time-View

    const routes: Routes = [
        {
            path: '',
            loadChildren: './time-view/time-view.module#TimeViewModule'
        }
    ];


entry Component in Entry-List benutzen (**entry-list.component.ts**)

    <time-entry></time-entry>


service für entries erstellen

    ng g s shared/services/entries




HttpModule

