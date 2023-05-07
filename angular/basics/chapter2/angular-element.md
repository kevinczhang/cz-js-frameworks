---
description: >-
  Angular elements are Angular components packaged as custom elements (also
  called Web Components), a web standard for defining new HTML elements in a
  framework-agnostic way.
---

# Angular element

Basically it will wrap the angular component into a JS file. When just load the JS file and then you can use the angular component in any Web app in most browsers.&#x20;

A custom element extends HTML by allowing you to define a tag whose content is created and controlled by JavaScript code. The browser maintains a `CustomElementRegistry` of defined custom elements, which maps an instantiable JavaScript class to an HTML tag.

&#x20;The `@angular/elements` package exports a [`createCustomElement`](https://angular.io/api/elements/createCustomElement)`()` API that provides a bridge from Angular's component interface and change detection functionality to the built-in DOM API.

## Using custom elements

Custom elements bootstrap themselves - they start automatically when they are added to the DOM, and are automatically destroyed when removed from the DOM.



