In TypeScript, you assign the value and type; then you must compile to JS in order to run in Browser.
> TS works well with Angular without the need to compile.

# Install Bootstrap:
  - npm install --save bootstrap@[version]
> run before you start your project (i.e. within gitbash terminal - after creating project folder and within that new project)
> _OR_ run in terminal of VS code (w/i proj)


## Learn NEW Angular #

angular.dev website – https://angular.dev/


## Angular Directives
- Directives perform tasks:
  - ngIf
  - ngFor
> i.e.:     ngif.components.ts 
>           ngif components.html

index.html file is what's running in browser (fr/ server)
>   runs fr/ <app-root>

main.ts -> passes an app.module.ts file, which then triggers the app.component 

## Ang App Components
- build components (comp's)
  - each comp's (i.e.: header, body, sidebar) -->
    - has it's own:
        - template
        - html code
        - styling <css> (if applicable)
        - business logic <ts>
> Generate new components fr/ VSC terminal:
   ng generate components
    |    |         |
   ng    g         c   **[name of component]*
- this creates new folder in your app folders w/ name of your 'new' component.
- will create same comp files as what's in your main app folder
- includes a ... spec.ts file (spec files used only for testing ... you can delete this file)
>  be sure to update your app.modules file w/ imports 
> **You can use your components multiple times in your code/project.*
  
- classes & decorators


## Databinding = Communication
TS Code (business Logic) --->output data  ---> HTML Template
> String Interpolation:  ({{**data*}})
> Property Binding:  ([**property*]='**data*)
> Event Binding:  ((**event*)='expression')
> Combo/Two-way Binding: ([(ngModel)]='**data*)
> >> React to (user) events

String Interp = any method or status that returns a string (or something that can be converted to a string) - i.e. number, methods, etc.

Property Binding vs String Interp
- if you want to output something (i.e. text) in your program >>> use string interp
- if you want to change some property (i.e.: html element, or directive, or component) >>> use property binding
>>> DO NOT MIX THE TWO!
- Property Binding - **NO CURLY BRACES**
  - [] sq brackets only
- Event Binding: uses ()
  - (click) => same as 'onClick'
  - Example:
      - <button
        - class = "btn btn-primary"
        - [disabled] = '!allowNewServer
        - (click) = "onCreateServer()"> Add Server </button>

($event) = give access to event data