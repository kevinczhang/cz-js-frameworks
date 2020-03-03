# Introduction to modules

Angular has its own modularity system called _NgModules_. NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities.

## 1. NgModule metadata

An NgModule is defined by a class decorated with @NgModule\(\).

The most important properties are as follows:

* **declarations:** The components, directives, and pipes that belong to this NgModule.
* **exports:** The subset of declarations that should be visible and usable in the component templates of other NgModules.
* **imports:** Other modules whose exported classes are needed by component templates declared in this NgModule.
* **providers:** Creators of services that this NgModule contributes to the global collection of services; they become accessible in all parts of the app. \(You can also specify providers at the component level, which is often preferred.\)
* **bootstrap:** The main application view, called the root component, which hosts all other app views. Only the root NgModule should set the bootstrap property.

### root NgModule sample

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## 2. NgModules and components

A NgModule can include any number of additional components, which can be loaded through the router or created through the template. The components that belong to an NgModule share a _compilation_ context provided by their NgModules.

When you create a component, it's associated directly with a single view, called the _host view_. The host view can be the root of a view hierarchy, which can contain _embedded views_, which are in turn the host views of other components.

