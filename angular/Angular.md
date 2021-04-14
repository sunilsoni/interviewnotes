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

