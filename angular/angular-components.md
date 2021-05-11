What Is an Angular Component?
==================

Angular Component = HTML Template + Component Class + Component Metadata

 <img src="./images-components/angular-component.png" width="300" border="2" />

Every Angular application has at least one component that is used to display the data on the view. Technically, a
component is nothing but a simple typescript class and composed of three things as follows:

    1. Class (Typescript class)
    2. Template (HTML Template or Template URL)
    3. Component Metadata (@Component Decorator)

Template:
-------------------
The template is used to define an interface with which the user can interact. As part of that template, you can define
HTML Mark-up; you can also define the directives, and bindings, etc. So in simple words, we can say that the template
renders the view of the application with which the end-user can interact i.e. user interface.

Class:
-------------------
The Class is the most important part of a component in which we can write the code which is required for a template to
render in the browser. You can compare this class with any object-oriented programming language classes such as C++, C#
or Java. The angular component class can also contain methods, variables, and properties like other programming
languages. The angular class properties and variables contain the data which will be used by a template to render on the
view. Similarly, the method in an angular class is used to implement the business logic like the method does in other
programming languages.

Component Metadata:
-------------------
Metadata is some extra data for a component used by Angular API to execute the component, such as the location of HTML
and CSS files of the component, selector, providers, etc.

`Note:` Whenever we create any component, we need to define that component in `@NgModule`.

Components are like the basic building block in an Angular application. Components are defined using the `@component`
decorator. A component has a `selector`, `template`, `style` and other properties, using which it specifies the metadata
required to process the component.

From the official docs:

> Components are the most basic building block of an UI in an Angular application. An Angular application is a tree of Angular components. 
Angular components are a subset of directives. Unlike directives, components always have a template and only one component can be instantiated per an element in a template.
 

Communication Between Components
-------------------------------

There are 4 ways to share data between components:

1. Parent to Child: Sharing Data via `Input`
2. Child to Parent: Sharing Data via `ViewChild` with `AfterViewInit`
3. Child to Parent: Sharing Data via `Output()` and `EventEmitter`
4. Unrelated Components: Sharing Data with a `Service`


- **Parent to Child: Sharing Data via Input**

It works by using the `@Input()` decorator to allow data to be passed via the template.

parent.component.ts

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [childMessage]="parentMessage"></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent{
  parentMessage = "message from parent"
  constructor() { }
}
```

child.component.ts

```typescript
import { Component, Input } from '@angular/core';

@Component({
    selector: 'app-child',
    template: `
      Say {{ message }}
  `,
    styleUrls: ['./child.component.css']
})
export class ChildComponent {

    @Input() childMessage: string;

    constructor() { }

}
```

- **Child to Parent: Sharing Data via ViewChild**

`ViewChild` allows a one component to be injected into another, giving the parent access to its attributes and functions. One caveat, however, is that child won’t be available until after the view has been initialized. This means we need to implement the `AfterViewInit` lifecycle hook to receive the data from the child.

parent.component.ts
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ChildComponent } from "../child/child.component";

@Component({
  selector: 'app-parent',
  template: `
    Message: {{ message }}
    <app-child></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent implements AfterViewInit {

  @ViewChild(ChildComponent) child;

  constructor() { }

  message:string;

  ngAfterViewInit() {
    this.message = this.child.message
  }
}

```

child.component.ts

```typescript
import { Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
  `,
  styleUrls: ['./child.component.css']
})
export class ChildComponent {

  message = 'Hola Mundo!';

  constructor() { }

}

```


- **Child to Parent: Sharing Data via Output() and EventEmitter**
  
Another way to share data is to emit data from the child, which can be listened to by the parent. This approach is ideal when you want to share data changes that occur on things like button clicks, form entires, and other user events.

In the parent, we create a function to receive the message and set it equal to the message variable.

In the child, we declare a messageEvent variable with the Output decorator and set it equal to a new event emitter. Then we create a function named sendMessage that calls emit on this event with the message we want to send. Lastly, we create a button to trigger this function.

The parent can now subscribe to this messageEvent that’s outputted by the child component, then run the receive message function whenever this event occurs.

parent.component.ts
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    Message: {{message}}
    <app-child (messageEvent)="receiveMessage($event)"></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent {

  constructor() { }

  message:string;

  receiveMessage($event) {
    this.message = $event
  }
}
```

child.component.ts

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
      <button (click)="sendMessage()">Send Message</button>
  `,
  styleUrls: ['./child.component.css']
})

export class ChildComponent {

  message: string = "Hola Mundo!"

  @Output() messageEvent = new EventEmitter<string>();

  constructor() { }

  sendMessage() {
    this.messageEvent.emit(this.message)
  }
}
```

- **Unrelated Components: Sharing Data with a Service**

When passing data between components that lack a direct connection, such as siblings, grandchildren, etc, you should you a shared service. When you have data that should aways been in sync, I find the RxJS BehaviorSubject very useful in this situation.

You can also use a regular RxJS Subject for sharing data via the service, but here’s why I prefer a `BehaviorSubject`.

- It will always return the current value on subscription - there is no need to call onnext
- It has a getValue() function to extract the last value as raw data.
- It ensures that the component always receives the most recent data.

In the service, we create a private `BehaviorSubject` that will hold the current value of the message. We define a currentMessage variable handle this data stream as an observable that will be used by the components. Lastly, we create function that calls next on the `BehaviorSubject` to change its value.

The parent, child, and sibling components all receive the same treatment. We inject the DataService in the constructor, then subscribe to the currentMessage observable and set its value equal to the message variable.

Now if we create a function in any one of these components that changes the value of the message. when this function is executed the new data it’s automatically broadcast to all other components.

data.service.ts
```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable()
export class DataService {

  private messageSource = new BehaviorSubject('default message');
  currentMessage = this.messageSource.asObservable();

  constructor() { }

  changeMessage(message: string) {
    this.messageSource.next(message)
  }

}
```
parent.component.ts


```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from "../data.service";
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-parent',
  template: `
    {{message}}
  `,
  styleUrls: ['./sibling.component.css']
})
export class ParentComponent implements OnInit, OnDestroy {

  message:string;
  subscription: Subscription;

  constructor(private data: DataService) { }

  ngOnInit() {
    this.subscription = this.data.currentMessage.subscribe(message => this.message = message)
  }
  
  ngOnDestroy() {
    this.subscription.unsubscribe();
  }

}
```

sibling.component.ts

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from "../data.service";
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-sibling',
  template: `
    {{message}}
    <button (click)="newMessage()">New Message</button>
  `,
  styleUrls: ['./sibling.component.css']
})
export class SiblingComponent implements OnInit, OnDestroy {

  message:string;
  subscription: Subscription;

  constructor(private data: DataService) { }

  ngOnInit() {
    this.subscription = this.data.currentMessage.subscribe(message => this.message = message)
  }

  ngOnDestroy() {
    this.subscription.unsubscribe();
  }

  newMessage() {
    this.data.changeMessage("Hello from Sibling")
  }

}
```


For more information:

1. [Angular Components with Examples](https://dotnettutorials.net/lesson/angular-components/)
2. [Angular Component](https://www.tutorialsteacher.com/angular/angular-component)
