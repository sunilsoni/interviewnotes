Angular Directive
==================


Directives are custom HTML attributes which tell angular to change the style or behavior of the Dom elements. When we
say that components are the building blocks of Angular applications, we are actually saying that directives are the
building blocks of Angular applications.

There are three kinds of directives:

1. Components Directives — directives with a template.
2. Structural Directives — change the DOM layout by adding and removing DOM elements.
3. Attribute Directives — change the appearance or behavior of an element, component, or another directive.

<img src="./images-directives/types-of-directives.png" width="400" border="2" />

Directives are instructions in the DOM (Document Object Model). It specifies how to place our business logic in Angular.
The directive is markers on a DOM element that tell Angular to attach a specified behavior to that DOM element or even
transform the DOM element and its children. Mostly directives in Angular starts with ng- where ng stands for Angular,
and it extends the HTML.

 <img src="./images-directives/dom-manipulation.png" width="400" border="2" />


Components Directives:
----------------

Components are the most common of the directives. It contains the details of how the component should be processed,
instantiated, and used at runtime. The component comprises meta-data.


Structural Directives:
----------------
Structural Directives are done in the elements section. These directives are used to manipulate and change the structure
of the DOM elements. Structural directives have a star (*) sign before the directive. Like as,* ngIf, *ngFor, and *
ngSwitch directive.

- `*ngIf Directive`: The `*ngIf` allows us to Add/Remove DOM Element.
- `*ngSwitch Directive`: The `*ngSwitch` will enable us to Add/Remove DOM element.
- `*ngFor Directive`: The `*ngFor` directive is used to repeat a part of HTML template once per each item from an
  iterable list (Collection).

Attribute Directives:
----------------

Itdeals with changing the look and behavior of the DOM element. For example: `ngClass`, `ngStyle` etc.

- NgClass Directive: The `ngClass` Directive is used to add or remove CSS classes to an element.
- NgStyle Directive: The `ngStyle` Directive facilitates you to modify the style of an HTML element using the
  expression. We can also use the `ngStyle` Directive to change the style of our HTML element dynamically

 <img src="./images-directives/Attributes-Directives.png" width="400" border="2" />


For more information:

1. [Angular 8 Directives](https://www.tutorialandexample.com/angular-8-directives/)

2. [Concepts Of Angular Directives](https://medium.com/@venkateshece1105/concepts-of-angular-directives-527ae0ca5995)
3. [A Practical Guide to Angular Directives](https://www.sitepoint.com/practical-guide-angular-directives/)
