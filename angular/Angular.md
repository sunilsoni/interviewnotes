What is Angular?
=================

Single-page application(SPA) vs. multiple-page application(MPA)
-----------

Single-Page Application
-----------
A single-page application is an app that works inside a browser and does not require page reloading during use. You are using this type of applications every day. These are, for instance: Gmail, Google Maps, Facebook or GitHub.

Pros of the Single-Page Application
-----------
- SPA is fast, as most resources (HTML+CSS+Scripts) are only loaded once throughout the lifespan of application. Only data is transmitted back and forth.
- The development is simplified and streamlined. There is no need to write code to render pages on the server. It is much easier to get started because you can usually kick off development from a file file://URI, without using any server at all.
- SPAs are easy to debug with Chrome, as you can monitor network operations, investigate page elements and data associated with it.
- It’s easier to make a mobile application because the developer can reuse the same backend code for web application and native mobile application.
- SPA can cache any local storage effectively. An application sends only one request, store all data, then it can use this data and works even offline.

Cons of the Single-Page Application
-----------
- It is very tricky and not an easy task to make SEO optimization of a Single-Page Application. Its content is loaded by AJAX (Asynchronous JavaScript and XML) — a method of exchanging data and updating in the application without refreshing the page.
- It is slow to download because heavy client frameworks are required to be loaded to the client.
- It requires JavaScript to be present and enabled. If any user disables JavaScript in his or her browser, it won’t be possible to present application and its actions in a correct way.
- Compared to the “traditional” application, SPA is less secure. Due to Cross-Site Scripting (XSS), it enables attackers to inject client-side scripts into web application by other users.
- Memory leak in JavaScript can even cause powerful system to slow down


Multiple-Page application(MPA)
-----------

Multiple-page applications work in a `traditional` way. Every change eg. display the data or submit data back to server requests rendering a new page from the server in the browser. These applications are large, bigger than SPAs because they need to be. Due to the amount of content, these applications have many levels of UI. 

Luckily, it’s not a problem anymore. Thanks to AJAX, 
we don’t have to worry that big and complex applications have to transfer a lot of data between server and browser. That solution improves and it allows to refresh only particular parts of the application. On the other hand, it adds more complexity and it is more difficult to develop than a single-page application.


Pros of the Multiple-Page Application
-----------
- It’s the perfect approach for users who need a visual map of where to go in the application. Solid, few level menu navigation is an essential part of traditional Multi-Page Application.
- Very good and easy for proper SEO management. It gives better chances to rank for different keywords since an application can be optimized for one keyword per page.

Cons of the multiple-page application
-----------
- There is no option to use the same backend with mobile applications.
- Frontend and backend development are tightly coupled.
- The development becomes quite complex. The developer needs to use frameworks for either client and server side. This results in the longer time of application development.

AngularJS vs Angular
-----------

Angular is a completely revived component-based framework in which an application is a tree of individual
components.


| AngularJS                                         | Angular                                             |
|---------------------------------------------------|-----------------------------------------------------|
|JavaScript-based framework for creating SPA.       |Complete re-write of AngularJS version.       |
|Still supported but no longer will be developed.   |It is updated version regularly released because of Semantic Versioning.|
|The architecture of AngularJS is based on MVC.     |The architecture of Angular 2 is component based|
|AngularJS was not developed with a mobile base in mind.|Angular 2 is a mobile-oriented framework.|
|AngularJS code can write by using only ES5, ES6, and Dart.|We can use ES5, ES6, Typescript to write an Angular 2 code.|
|Factory, service, provider, value and constant are used for services|The class is the only method to define services in Angular2|
|Run on only client-side                             |Runs on client-side & server-side|
|ng-app and angular bootstrap function are used to initialize | bootstrapmodule() function is used to initialize|

**a.) AngularJS**
-----------


**Advantages**

* It has great MVC data binding that makes app development fast.
* Using HTML as a declarative language makes it very intuitive.
* It is a comprehensive solution for rapid front-end development since it does not need any other frameworks or plugins.
* AngularJS apps can run on every significant program and advanced cells including iOS and Android-based phones and tablets.
* Two-way data binding
* Directives
* Dependency injection

**Disadvantages**

* It is big and complicated due to the multiple ways of doing the same thing.
* Implementations scale poorly.
* If a user of an AngularJS application disables JavaScript, nothing but the basic page is visible.
* There is a lagging UI if there are more than 200 watchers.


**b.) Angular**
-----------


**Advantages**

* Component-based architecture that provides a higher quality of code
* Reusability: Components of similar nature are well encapsulated, in other words, self-sufficient. Developers can reuse them across different parts of an application.
* Unit-test friendly: The independent nature of components simplifies unit tests, quality assurance procedures aimed at verifying the performance of the smallest parts of the application, units.
* Maintainability: Components that are easily decoupled from each other can be easily replaced with better implementations.


**Disadvantages**

* Angular is verbose and complex
* Steep learning curve
* Migrating legacy systems from AngularJS to Angular requires time

Why Angular
-----------

Angular is a development platform, built on TypeScript. As a platform, Angular includes:

* A component-based framework for building scalable web applications
* A collection of well-integrated libraries that cover a wide variety of features, including routing, forms management,
  client-server communication, and more
* A suite of developer tools to help you develop, build, test, and update your code

With Angular, you're taking advantage of a platform that can scale from single-developer projects to enterprise-level
applications. Angular is designed to make updating as easy as possible, so you can take advantage of the latest
developments with a minimum of effort.

Components
-----------------
Components are a logical piece of code for Angular application. A Component consists −

- **Template** This is used to render the view for the application. This contains the HTML that needs to be rendered in
  the application. This part also includes the binding and directives.
- **Class** This is like a class defined in any language such as C. This contains properties and methods. This has the
  code which is used to support the view. It is defined in TypeScript.
- **Metadata** This has the extra data defined for the Angular class. It is defined with a decorator.

Components are the building blocks that compose an application. A component includes a TypeScript class with a
@Component() decorator, an HTML template, and styles. The [@Component()](https://angular.io/api/core/Component)
decorator specifies the Angular-specific information:

- A CSS selector that defines how the component is used in a template. HTML elements in your template that match this
  selector become instances of the component.
- An HTML template that instructs Angular how to render the component.
- An optional set of CSS styles that define the appearance of the template's HTML elements.

The following is a minimal Angular component.

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
<h2>Hello World</h2>
<p>This is my first component!</p>
`,
})
export class HelloWorldComponent {
// The code in this class drives the component's behavior.
}
```

To use this component, you write the  in a template:

```typescript
<hello-world > </hello-world>
```

When Angular renders this component, the resulting DOM looks like this:

```typescript
<hello-world >
<h2>Hello
World < /h2>
< p > This
is
my
first
component! < /p>
< /hello-world>
```

Angular's component model offers strong encapsulation and an intuitive application structure. Components also make your
application easier to unit test and can improve the overall readability of your code.


Templates
-----------------
Every component has an HTML template that declares how that component renders. You define this template either inline or
by file path.

Angular extends HTML with additional syntax that lets you insert dynamic values from your component. Angular
automatically updates the rendered DOM when your component’s state changes. One application of this feature is inserting
dynamic text, as shown in the following example.

```typescript
<p>{
{
  message
}
}
</p>
```

The value for message comes from the component class:

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
})
export class HelloWorldInterpolationComponent {
  message = 'Hello, World!';
}
```

When the application loads the component and its template, the user sees:

```typescript
<p>Hello, World! < /p>
```

Notice the use of double curly braces--they instruct Angular to interpolate the contents within them.

Angular also supports property bindings, to help you set values for properties and attributes of HTML elements and pass
values to your application's presentation logic.

```typescript
<p [id] = "sayHelloId" [style.color] = "fontColor" > You
can
set
my
color in the
component! < /p>
```

Notice the use of the square brackets--that syntax indicates that you're binding the property or attribute to a value in
the component class.

You can also declare event listeners to listen for and respond to user actions such as keystrokes, mouse movements,
clicks, and touches. You declare an event listener by specifying the event name in parentheses:

```typescript
<button (click) = "sayMessage()" [disabled] = "canClick" > Trigger
alert
message < /button>
```

The preceding example calls a method, which is defined in the component class:

```typescript
sayMessage()
{
  alert(this.message);
}
```

hello-world-bindings.component.ts

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-bindings',
  templateUrl: './hello-world-bindings.component.html'
})
export class HelloWorldBindingsComponent {
  fontColor = 'blue';
  sayHelloId = 1;
  canClick = false;
  message = 'Hello, World';

  sayMessage() {
    alert(this.message);
  }
}
```

hello-world-bindings.component.html

```html

<button (click)="sayMessage()" [disabled]="canClick">Trigger alert message</button>
<p [id]="sayHelloId" [style.color]="fontColor">You can set my color in the component!</p>

```

You can add additional functionality to your templates through the use of directives. The most popular directives in
Angular are <B>*ngIf</B> and <B>*ngFor</B>. You can use directives to perform a variety of tasks, such as dynamically
modifying the DOM structure. And you can also create your own custom directives to create great user experiences.

The code is an example of the *ngIf directive.

hello-world-ngif.component.ts

```typescript

import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-ngif',
  templateUrl: './hello-world-ngif.component.html'
})
export class HelloWorldNgIfComponent {
  message = 'I\'m read only!';
  canEdit = false;

  onEditClick() {
    this.canEdit = !this.canEdit;
    if (this.canEdit) {
      this.message = 'You can edit me!';
    } else {
      this.message = 'I\'m read only!';
    }
  }
}

```

hello-world-ngif.component.html

```html

<h2>Hello World: ngIf!</h2>
<button (click)="onEditClick()">Make text editable!</button>
<div *ngIf="canEdit; else noEdit">
  <p>You can edit the following paragraph.</p>
</div>
<ng-template #noEdit>
  <p>The following paragraph is read only. Try clicking the button!</p>
</ng-template>
<p [contentEditable]="canEdit">{{ message }}</p>

```

Angular's declarative templates allow you to cleanly separate your application's logic from its
presentation.  [Templates](https://angular.io/guide/template-syntax) are based on standard HTML, so they're easy to
build, maintain, and update.


Dependency injection
-----------------

Dependency Injection (DI) allows a class receive dependencies from another class. Most of the time in Angular, dependency injection is done by injecting a service class into a component or module class.

```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class PopcornService {

  constructor() {
    console.log("Popcorn has been injected!");
  }

  cookPopcorn(qty) {
    console.log(qty, "bags of popcorn cooked!");
  }
}
```
*AppComponent.ts*
```typescript
import { Component } from '@angular/core';
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  providers: [PopcornService]
})
export class AppComponent {
  constructor(private popcorn: PopcornService) {}

  cookIt(qty) {
    this.popcorn.cookPopcorn(qty);
  }
}
```


Dependency injection allows you to declare the dependencies of your TypeScript classes without taking care of their
instantiation. Instead, Angular handles the instantiation for you. This design pattern allows you to write more testable
and flexible code. Even though understanding dependency injection is not critical to start using Angular, we strongly
recommend it as a best practice and many aspects of Angular take advantage of it to some degree.

To illustrate how dependency injection works, consider the following example. The first file, logger.service.ts, defines
a Logger class. This class contains a writeCount function that logs a number to the console.

logger.service.ts

```typescript
import {Injectable} from '@angular/core';

@Injectable({providedIn: 'root'})
export class Logger {
  writeCount(count: number) {
    console.warn(count);
  }
}
```

Next, the hello-world-di.component.ts file defines an Angular component. This component contains a button that uses the
writeCount function of the Logger class. To access that function, the Logger service is injected into the HelloWorldDI
class by adding private logger: Logger to the constructor.

hello-world-di.component.ts

```typescript
import {Component} from '@angular/core';
import {Logger} from '../logger.service';

@Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
})
export class HelloWorldDependencyInjectionComponent {
  count = 0;

  constructor(private logger: Logger) {
  }

  onLogMe() {
    this.logger.writeCount(this.count);
    this.count++;
  }
}
```

For more information  [Dependency injection ](https://angular.io/guide/dependency-injection)

What is routing
-----------------

- A website is made up of a multitude of pages These pages are written with HTML(HyperText Markup Language) language.
- Hypertext is the technology that will link a page to other pages via hyperlinks.
- Routing is the mechanism for navigating from one page to another on a website.

For example, if you type these two urls in your browser.

```html
https://en.wikipedia.org/wiki/Braveheart
https://en.wikipedia.org/wiki/Dances_with_Wolves
```

Depending on the movie name indicated in the url, the Wikipedia web application will determine the processing to be
performed. This treatment will display the web page corresponding to the requested movie (here  `Braveheart`
or `Dances_with_Wolves` ).

This is called Routing.

Angular Routing and Navigation
-----------------

- The `Angular Router enables navigation from one view (component)` to the another/next as users perform tasks, views (
  component)
- Routing simply means navigating between different view (component)
- **RouterModule**
  - RouterModule helps to `create routes`, which allows us to move from one part of the application to another part or
    from one view to another
  - A separate NgModule/Angular Module that provides the necessary service providers and directives for navigating
    through application views
- **Router**
  - The Angular Router is an `optional service that presents a particular component view` for a given URL, it is not
    part of the Angular core
  - The Angular Router enables navigation from one view to the another as users perform application tasks/actions
- **router-outlet**
  - The directive `(<router-outlet>)` that marks where the router displays a view (a container to hold different
    views/components loaded as users perform application tasks/actions)
- **routerLink**
  - The attribute/directive for binding a clickable HTML element to a route which denotes link/view name to load/show
    in `(<router-outlet>)`



Angular Module
-----------------

In Angular, a module is a mechanism to group components, directives, pipes and services that are related, in such a way that can be combined with other modules to create an application.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule ({
    imports:      [ BrowserModule ],
    declarations: [ AppComponent ],
    bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

The NgModule decorator has three options
* The imports option is used to import other dependent modules. The BrowserModule is required by default for any web based angular application
* The declarations option is used to define components in the respective module
* The bootstrap option tells Angular which Component to bootstrap in the application


What is Interpolation?
------------------

Interpolation is a special syntax that Angular converts into property binding. It is a convenient alternative to property binding. It is represented by double curly braces(`{{ }}`). The text between the braces is often the name of a component property. Angular replaces that name with the string value of the corresponding component property.

```html
<h3>
  {{title}}
  <img src="{{url}}" style="height:30px">
</h3>
```

In the example , Angular evaluates the title and url properties and fills in the blanks, first displaying a bold application title and then a URL.

Bootstrapping Module
------------------

Every application has at least one Angular module, the root module that you bootstrap to launch the application is called as bootstrapping module. It is commonly known as AppModule. The default structure of AppModule generated by AngularCLI would be as follows,

```typescript
/* JavaScript imports */
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

/* the AppModule class with the @NgModule decorator */
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

JIT vs AOT compilation
---------------------

Angular has 2 types of build dev build or prod build

**JIT**  
Just-in-Time (JIT) is a type of compilation that compiles app in the browser at runtime. JIT compilation is the default when you run the ng build (build only) or ng serve (build and serve locally) CLI commands. i.e, the below commands used for JIT compilation,

```javascript
ng build
ng serve
```
**AOT**  
Ahead-of-Time (AOT) is a type of compilation that compiles app at build time. For AOT compilation, include the `--aot` option with the ng build or ng serve command as below,

```javascript
ng build --aot
ng serve --aot
```

```
ng build or ng build --dev   -  this is for development build
ng build --prod              -  this is for production build
```

|Dev Build	                                |Production build                           |
|-------------------------------------------|-------------------------------------------|
|Source maps(.js.map files) are generated	  |Source maps not generated                  |
|Dev Build is not minified and uglified	    |Production Build is minified and uglified  |
|Dev build is not tree shaked	              |Production build is tree shaked            |
|No AOT compilation	                        |AOT compilation takes place                |


* **minification** - process of removing excess whitespace, comments and optinal tokens like curly braces and semi colons
* **uglification** - process of transforming code to use short variable and function names
* **tree shaking** -  is the process of removing any code that we are not actually using in our application from the final bundle

*Note: The ng build command with the --prod meta-flag (`ng build --prod`) compiles with AOT by default.*


Advantages of AOT
----------------

1. **Faster rendering** The browser downloads a pre-compiled version of the application. So it can render the application immediately without compiling the app.
2. **Fewer asynchronous requests** It inlines external HTML templates and CSS style sheets within the application javascript which eliminates separate ajax requests.
3. **Smaller Angular framework download size** Does not require downloading the Angular compiler. Hence it dramatically reduces the application payload.
4. **Detect template errors earlier** Detects and reports template binding errors during the build step itself
5. **Better security** It compiles HTML templates and components into JavaScript.  So there wont be any injection attacks.


What are the ways to control AOT compilation?
----------------


You can control your app compilation in two ways
1. By providing template compiler options in the `tsconfig.json` file
2. By configuring Angular metadata with decorators


How to optimize loading large data in angular?
---------------

**Load Time Performance**

1. **AOT**: The Angular Ahead-of-Time (AOT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript code during the build phase before the browser downloads and runs that code. Compiling your application during the build process provides a faster rendering in the browser.
2. **Tree-shaking**: This is the process of removing unused code resulting in smaller build size. In **angular-cli**, Tree-Shaking is enabled by default.
3. **Uglify**: It is the process where the code size is reduced using various code transformations like mangling, removal of white spaces, removal of comments etc. For webpack use uglify plugin and with angular-cli specify the "prod" flag to perform the uglification process.
4. **Lazy loading**: Lazy loading is the mechanism where instead of loading complete app, we load only the modules which are required at the moment thereby reducing the initial load time.
5. **Ivy Render Engine**: It results in much smaller bundle size than the current engine with improved debugging experience.
6. **RxJS**: RxJS makes the whole library more tree-shakable thereby reducing the final bundle size. However, it has some breaking changes like operators chaining is not possible instead, pipe() function (helps in better tree shaking) is introduced to add operators.
7. **Service worker cache**: A service worker is a script that runs in the web browser and manages caching for an application.
8. **defer attribute**: Mentioning defer attribute to script tag will defer the loading of the scripts (sychronous) until the document is not parsed thus making site interactive quicker.
9. **async attribute**: async delays the loading of scripts until the document is not parsed but without respecting the order of loading of the scripts.
10. **ChangeDetectionStrategy.OnPush**: `ChangeDetectionStrategy.OnPush` tells Angular that the component only depends on his Inputs ( aka pure ) and needs to be checked in only the following cases:  
    i). The `Input` reference changes.  
    ii). An event occurred from the component or one of his children.  
    iii). You run change detection explicitly by calling `detectChanges()/tick()/markForCheck()`

Example

```typescript
@Component({
  selector: 'my-select',
  template: `
    ...
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
```

11. **TrackBy**: If we provide a trackBy function, Angular can track which items have been added or removed according to the unique identifier and only create or destroy the things that have changed.

Example:

```typescript
@Component({
  selector: 'my-app',
  template: `
    <ul>
      <li *ngFor="let item of collection;trackBy: trackByFn">{{item.id}}</li>
    </ul>
    <button (click)="getItems()">Refresh items</button>
  `,
})
export class App {

  constructor() {
    this.collection = [{id: 1}, {id: 2}, {id: 3}];
  }
  getItems() {
    this.collection = this.getItemsFromServer();
  }
  getItemsFromServer() {
    return [{id: 1}, {id: 2}, {id: 3}, {id: 4}];
  }
  trackByFn(index, item) {
    return index; // or item.id
  }
}
```



How an Angular application gets started or loaded?
------------

The **main.ts** file, that is the first code which gets executed. The job of main.ts is to bootstrap the application. It loads everything and controls the startup of the application.

**main.ts**

```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

Most importantly here is the line where bootstraps start our angular app by passing app module to the method. AppModule refers to the app.module.ts file.

**app.module.ts**

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, ErrorHandler } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [ ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

When angular starts, it bootstrap array in `@NgModule`. It basically there is a list of all components which should be known to Angular at the point of time it analyzes **index.html** file.

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Angular 8</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
  </head>
  <body>
    <app-root>Loading...</app-root>
  </body>
</html>
```

For more information:

1. [Angular Routing and Navigation](https://github.com/sunilsoni/interview-notes/blob/main/angular/angular-routing.md#1-angular-routing-and-navigation)
2. [Routing and navigation with Angular 11](https://www.ganatan.com/tutorials/routing-with-angular)

