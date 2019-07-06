---
description: >-
  A provider is an instruction to the DI system on how to obtain a value for a
  dependency. Most of the time, these dependencies are services that you create
  and provide.
---

# Providers

## Provider scope

[`providedIn`](https://angular.io/api/core/Injectable#providedIn)`: 'root'` specifies that the service should be provided in the root injector.  When you add a service provider to the root application injector, it’s available throughout the app. Additionally, these providers are also available to all the classes in the app as long they have the lookup token.

 It's also possible to specify that a service should be provided in a particular `@`[`NgModule`](https://angular.io/api/core/NgModule).

```typescript
import { Injectable } from '@angular/core';
import { UserModule } from './user.module';

@Injectable({
  providedIn: UserModule,
})
export class UserService {
}
```

### Limiting provider scope by lazy loading modules <a id="limiting-provider-scope-by-lazy-loading-modules"></a>

 In the basic CLI-generated app, modules are eagerly loaded which means that they are all loaded when the app launches. 

 Lazy loading is when you load modules only when you need them; for example, when routing.  When the Angular router lazy-loads a module, it creates a new injector. This injector is a child of the root application injector. 

### Limiting provider scope with components <a id="limiting-provider-scope-with-components"></a>

```typescript
@Component({
/* . . . */
  providers: [UserService]
})
```

##  Singleton services

### Providing a singleton service <a id="providing-a-singleton-service"></a>

There are two ways to make a service a singleton in Angular:

* Declare that the service should be provided in the application root.
* Include the service in the `AppModule` or in a module that is only imported by the `AppModule`.

## forRoot\(\) and forChild\(\)

Angular provides a way to separate providers out of the module so that same module can be imported into the root module with `providers` and child modules without `providers`.

1. Create a static method [`forRoot()`](https://angular.io/api/router/RouterModule#forRoot) \(by convention\) on the module.
2. Place the providers into the `forRoot` method as follows.

Essentially, forRoot and forChild allow us to have control of the provider \(our injectable\) depending on the type of load we want to give them. This allows us to have different configurations for different load cases.

 ForRoot is used when a module is "eager," that is, it is not lazy-loaded \(loads when the application starts\). Angular creates a factory for all the modules, except for the lazy modules, which when loaded on demand, have their own factory. When we use forRoot\(\), we’re loading a provider that is going to be injected into the "root" of the modules because it uses the same factory as our main module.

ForChild is used the other way around: specifically when we want to deliver a provider that is visible only to the "children" modules of our module, in case they are lazy loaded. As each lazy module is loaded on demand, it has its own injector.

 Beyond the usage of control what we instantiate when importing our modules, forRoot and forChild offer us something much more useful. It allows us to inject configurations to our modules. 

## Prevent reimport of the `CoreModule`

 Only the root `AppModule` should import the `CoreModule`. To guard against a lazy-loaded module re-importing `CoreModule`, add the following `CoreModule`constructor.

```typescript
constructor (@Optional() @SkipSelf() parentModule: CoreModule) {
  if (parentModule) {
    throw new Error(
      'CoreModule is already loaded. Import it in the AppModule only');
  }
}
```



