---
description: >-
  NgModules configure the injector and the compiler and help organize related
  things together.
---

# NgModules

## Purpose of @NgModule

The metadata falls into three categories:

* **Static:** Compiler configuration which tells the compiler about directive selectors and where in templates the directives should be applied through selector matching. This is configured via the [`declarations`](https://angular.io/api/core/NgModule#declarations) array.
* **Runtime:** Injector configuration via the `providers` array.
* **Composability/Grouping:** Bringing NgModules together and making them available via the [`imports`](https://angular.io/api/core/NgModule#imports)and [`exports`](https://angular.io/api/core/NgModule#exports) arrays.

```typescript
@NgModule({
  // Static, that is compiler configuration
  declarations: [], // Configure the selectors
  entryComponents: [], // Generate the host factory

  // Runtime, or injector configuration
  providers: [], // Runtime injector configuration

  // Composability / Grouping
  imports: [], // composing NgModules together
  exports: [] // making NgModules available to other parts of the app
})
```

##   JavaScript Modules vs. NgModules

* An NgModule bounds [declarable classes](https://angular.io/guide/ngmodule-faq#q-declarable) only. Declarables are the only classes that matter to the [Angular compiler](https://angular.io/guide/ngmodule-faq#q-angular-compiler).
* Instead of defining all member classes in one giant file as in a JavaScript module, you list the module's classes in the `@`[`NgModule.declarations`](https://angular.io/api/core/NgModule#declarations) list.
* An NgModule can only export the [declarable classes](https://angular.io/guide/ngmodule-faq#q-declarable) it owns or imports from other modules. It doesn't declare or export any other kind of class.
* Unlike JavaScript modules, an NgModule can extend the _entire_ application with services by adding providers to the `@`[`NgModule.providers`](https://angular.io/api/core/NgModule#providers) list.

##  Frequently Used Modules

| NgModule | Import it from | Why you use it |
| :--- | :--- | :--- |
| [`BrowserModule`](https://angular.io/api/platform-browser/BrowserModule) | `@angular/platform-browser` | When you want to run your app in a browser |
| [`CommonModule`](https://angular.io/api/common/CommonModule) | `@angular/common` | When you want to use [`NgIf`](https://angular.io/api/common/NgIf), `NgFor` |
| [`FormsModule`](https://angular.io/api/forms/FormsModule) | `@angular/forms` | When you want to build template driven forms \(includes [`NgModel`](https://angular.io/api/forms/NgModel)\) |
| [`ReactiveFormsModule`](https://angular.io/api/forms/ReactiveFormsModule) | `@angular/forms` | When you want to build reactive forms |
| [`RouterModule`](https://angular.io/api/router/RouterModule) | `@angular/router` | When you want to use [`RouterLink`](https://angular.io/api/router/RouterLink), `.forRoot()`, and `.forChild()` |
| [`HttpClientModule`](https://angular.io/api/common/http/HttpClientModule) | `@angular/common/`[`http`](https://angular.io/api/common/http) | When you want to talk to a server |

## Entry Components

 An entry component is any component that Angular loads imperatively.  You specify an entry component by bootstrapping it in an NgModule, or including it in a routing definition.

There are two main kinds of entry components:

* The bootstrapped root component.
* A component you specify in a route definition.

#### `entryComponents` and the compiler <a id="entrycomponents-and-the-compiler"></a>

 For production apps you want to load the smallest code possible. The code should contain only the classes that you actually need and exclude components that are never used. For this reason, the Angular compiler only generates code for components which are reachable from the `entryComponents`; This means that adding more references to `@`[`NgModule.declarations`](https://angular.io/api/core/NgModule#declarations) does not imply that they will necessarily be included in the final bundle.

##  NgModule FAQs

[https://angular.io/guide/ngmodule-faq](https://angular.io/guide/ngmodule-faq)

