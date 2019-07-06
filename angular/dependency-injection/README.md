# Dependency Injection

### Create and register an injectable service <a id="create-and-register-an-injectable-service"></a>

#### Create an injectable service class \(ng generate service heroes/hero\) <a id="create-an-injectable-service-class"></a>

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class HeroService {
  constructor() { }
}
```

The class we have created provides a service. The `@`[`Injectable`](https://angular.io/api/core/Injectable)`()` decorator marks it as a service that can be injected, but Angular can't actually inject it anywhere until you configure an Angular [dependency injector](https://angular.io/guide/glossary#injector) with a [provider](https://angular.io/guide/glossary#provider) of that service.

The injector is responsible for creating service instances and injecting them into classes like `HeroListComponent`.

### Injecting services <a id="injecting-services"></a>

 You can tell Angular to inject a dependency in a component's constructor by specifying a **constructor parameter with the dependency type**.

Services are singletons _within the scope of an injector_. That is, there is at most one instance of a service in a given injector. There is only one root injector for an app.

Child modules and component injectors are independent of each other, and create their own separate instances of the provided services. When Angular destroys an NgModule or component instance, it also destroys that injector and that injector's service instances.

## Dependency injection tokens

 When you configure an injector with a provider, you associate that provider with a [DI token](https://angular.io/guide/glossary#di-token). The injector maintains an internal _token-provider_ map that it references when asked for a dependency. The token is the key to the map.

#### Optional dependencies <a id="optional-dependencies"></a>

 When a component or service declares a dependency, the class constructor takes that dependency as a parameter. You can tell Angular that the dependency is optional by annotating the constructor parameter with `@`[`Optional`](https://angular.io/api/core/Optional)`()`.

```typescript
constructor(@Optional() private logger: Logger) {
  if (this.logger) {
    this.logger.log(some_message);
  }
}
```

