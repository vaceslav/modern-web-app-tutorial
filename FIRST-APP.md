# First Angular App

1. create git repository
1. prepare instructions  

        install yarn  
        yarn global add  @angular/cli  
        ng config -g cli.packageManager yarn  
1. create new angular project  

        ng new ntt-time --routing --prefix time --style sass

1. push to git  

        git remote add origin https://github.com/vaceslav/ntt-time.git  
        git push -u origin master  
        `username and password`
1. create branch for development


## Development

    yarn start

1. remove unused content
1. edit vs code settings

        "[typescript]": {
            "editor.formatOnSave": true
        }
1. create .prettierrc

        {
            "printWidth": 120,
            "singleQuote": true
        }
1. create new component: TimeEntry
        
        ng g c components/entry
1. create new component: TimeEntryList  

        ng g c components/entry-list

1. create @Input()'s 
1. create dummy data
1. create button: **add item**

## Add Material Design

    yarn add @angular/material @angular/cdk

add ButtonModule

        <button (click)="addItemClick()">Add Item</button>
extend style

        @import "~@angular/material/prebuilt-themes/deeppurple-amber.css";  


    <button mat-raised-button color="primary" (click)="addItemClick()">Add Item</button>


create some styles for entry
