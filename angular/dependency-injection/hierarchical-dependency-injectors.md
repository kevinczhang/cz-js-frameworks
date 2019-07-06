---
description: >-
  The Angular dependency injection system is hierarchical. There is a tree of
  injectors that parallel an app's component tree.
---

# Hierarchical Dependency Injectors

 The choices you make about where to configure providers lead to differences in the final bundle size, service _scope_, and service _lifetime_.  For both root-level and module-level injectors, a service instance lives for the life of the app or module, and Angular injects this one service instance in every class that needs it.

1.  Platform injector:  When you use [`providedIn`](https://angular.io/api/core/Injectable#providedIn)`:'root'`, you are configuring the root injector for the _app_, which is the injector for `AppModule`. The actual root of the entire injector hierarchy is a _platform injector_ that is the parent of app-root injectors. This allows multiple apps to share a platform configuration.
2.  _NgModule-level_ providers:  can be specified with `@`[`NgModule`](https://angular.io/api/core/NgModule)`()` `providers` metadata option, or in the `@`[`Injectable`](https://angular.io/api/core/Injectable)`()` [`providedIn`](https://angular.io/api/core/Injectable#providedIn) option \(with some module other than the root `AppModule`\).  Use the `@`[`NgModule`](https://angular.io/api/core/NgModule)`()` `provides` option if a module is [lazy loaded](https://angular.io/guide/lazy-loading-ngmodules).  The module's own injector is configured with the provider when that module is loaded, and Angular can inject the corresponding services in any class it creates in that module. If you use the `@`[`Injectable`](https://angular.io/api/core/Injectable)`()`option [`providedIn`](https://angular.io/api/core/Injectable#providedIn)`: MyLazyloadModule`, the provider could be shaken out at compile time, if it is not used anywhere else in the app.
3.  _Component-level_ providers:  configure each component instance's own injector. Angular can only inject the corresponding services in that component instance or one of its descendant component instances. Angular can't inject the same service instance anywhere else.  A component-provided service may have a limited lifetime. Each new instance of the component gets its own instance of the service. When the component instance is destroyed, so is that service instance.

#### @NgModule-level injectors <a id="ngmodule-level-injectors"></a>

```typescript
providers: [
  { provide: LocationStrategy, useClass: HashLocationStrategy }
]
```

#### @Component-level injectors <a id="component-level-injectors"></a>

```typescript
import { Component } from '@angular/core';

import { HeroService } from './hero.service';

@Component({
  selector: 'app-heroes',
  providers: [ HeroService ],
  template: `
    <h2>Heroes</h2>
    <app-hero-list></app-hero-list>
  `
})
export class HeroesComponent { }
```

[Nice article related to Injector](https://blog.angularindepth.com/a-curios-case-of-the-host-decorator-and-element-injectors-in-angular-582562abcf0a)

## Injector bubbling

When a component requests a dependency, Angular tries to satisfy that dependency with a provider registered in that component's own injector. If the component's injector lacks the provider, it passes the request up to its parent component's injector. If that injector can't satisfy the request, it passes the request along to the next parent injector up the tree. The requests keep bubbling up until Angular finds an injector that can handle the request or runs out of ancestor injectors. If it runs out of ancestors, Angular throws an error. If you have registered a provider for the same DI token at different levels, the first one Angular encounters is the one it uses to provide the dependency.

{% hint style="info" %}
 You can cap the bubbling by adding the `@`[`Host`](https://angular.io/api/core/Host)`()` parameter decorator on the dependant-service parameter in a component's constructor. The hunt for providers stops at the injector for the host element of the component.
{% endhint %}

## Component injectors

1. **Scenario: service isolation**
2. **Scenario: multiple edit sessions**
3. **Scenario: specialized providers**

![](../../.gitbook/assets/image%20%281%29.png)

