What is Angular?
=================

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

To use this component, you write the following in a template:

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

When the application loads the component and its template, the user sees the following:

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

The following code is an example of the *ngIf directive.

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

For more
information  [Angular Routing and Navigation](https://github.com/sunilsoni/interview-notes/blob/main/angular/angular-routing.md#1-angular-routing-and-navigation)

