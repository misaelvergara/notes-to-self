 What is Angular?
----
Angular is a framework that builds front-end user interfaces for web applications. Mix static html code and dynamic things we want to output in that code.

A component always has:
- a template (the html code);
- styling (scss);
- a typescript file.

**`Data Binding`**  _**[? vinculação|união de dados]**_ enables data to be outputted dynamically in a template.
**`Directive`**  [(ngModel)] listens to an input and stores the value in a property. Also, on the other hand, outputs the property to the input field.


- Angular 1 is referred to as AngularJS, which is a separate framework from Angular.	

[Lazy Loading, Design Pattern, ]

Getting Started On The CLI
---
`npm install -g @angular/cli@latest`
`npm new <app-name>`
`ng serve`

Angular Native Modules
---
Angular is split into multiple modules, subpackages, you could say. So, in order to make use of a specific feature, the module that contains that feature must be imported.
Modules are were you tell Angular which pieces belong to our app.

Angular Initialization
---
The first file that's read is `main.ts`, which imports `app-module.ts`, passing `AppModule` as a parameter to `platformBrowserDynamic.bootstrapModule()`. The App module has a `bootstrap` array that lists all the components which should be known to Angular upon initialization. AppComponent is one of them.


**`Lazy Loading`** is a design pattern used to defer _**[? to postpone, adiar, diferir]**_ initialization of an object until it is needed. The opposite of lazy loading is eager loading.
**`Node.JS`** is a server-side language.
**`Workflow`** _**[? fluxo de trabalho]**_ the sequence of industrial, administrative, or other processes through which a piece of work passes from initiation to completion.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4NTY1Njc4XX0=
-->