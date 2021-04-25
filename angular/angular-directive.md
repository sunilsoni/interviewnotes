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

Every component has Input and Output option to pass between component and its parent HTML elements.

```html

<component-selector-name [input-reference]="input-value"> ...</component-selector-name>
```

For example,

```html

<list-item [items]="fruits"> ...</list-item>
```

Here, list-item is a component and items is the input option. We will learn how to create component and advanced usages
in the later chapters.


Structural Directives:
----------------
Structural Directives are done in the elements section. These directives are used to manipulate and change the structure
of the DOM elements. Structural directives have a star (*) sign before the directive. Like as,* ngIf, *ngFor, and *
ngSwitch directive.

- `*ngIf Directive`: The `*ngIf` allows us to Add/Remove DOM Element.
- `*ngSwitch Directive`: The `*ngSwitch` will enable us to Add/Remove DOM element.
- `*ngFor Directive`: The `*ngFor` directive is used to repeat a part of HTML template once per each item from an
  iterable list (Collection).

```html

<HTMLTag [structuralDirective]='value'/>
```

For example,

```html

<div *ngIf="isNeeded">
  Only render if the *isNeeded* value has true value.
</div>
```

Here, `ngIf` is a built-in directive used to add or remove the HTML element in the current HTML document.

Attribute Directives:
----------------

It deals with changing the look and behavior of the DOM element. For example: `ngClass`, `ngStyle` etc.

- NgClass Directive: The `ngClass` Directive is used to add or remove CSS classes to an element.
- NgStyle Directive: The `ngStyle` Directive facilitates you to modify the style of an HTML element using the
  expression. We can also use the `ngStyle` Directive to change the style of our HTML element dynamically

 <img src="./images-directives/Attributes-Directives.png" width="600" border="2" />

```html

<HTMLTag [attrDirective]='value'/>
```

For example,

```html 
<p [showToolTip]='Tips' />
```

Here, `showToolTip` refers an example directive, which when used in a HTML element will show tips while user hovers the
HTML element.

Difference between Structural Directive and Attribute Directive
----------------

|  Structural Directive       |  Attribute Directive  |
| ----------- | ----------- |
| Structural directives are applied to `<template>` elements and used to add or remove content (stamp and template).      | The component has their view (HTML and styles) because of that, there can be one component on a host element, but multiple directives.       |

How to Create Custom Directives?
----------------

We can create our custom directives to use in Angular components with the help of the command line. The command which is
used to develop the Directive using the command line is as follows-

For more information:

1. [Angular 8 Directives](https://www.tutorialandexample.com/angular-8-directives/)
2. [Angular 8 - Directives](https://www.tutorialspoint.com/angular8/angular8_directives.htm)
3. [Concepts Of Angular Directives](https://medium.com/@venkateshece1105/concepts-of-angular-directives-527ae0ca5995)
4. [A Practical Guide to Angular Directives](https://www.sitepoint.com/practical-guide-angular-directives/)
