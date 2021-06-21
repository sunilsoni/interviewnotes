What is Angular?
=================

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


For more information:

1. [Angular Routing and Navigation](https://github.com/sunilsoni/interview-notes/blob/main/angular/angular-routing.md#1-angular-routing-and-navigation)
2. [Routing and navigation with Angular 11](https://www.ganatan.com/tutorials/routing-with-angular)

