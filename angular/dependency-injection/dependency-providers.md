---
description: >-
  A dependency provider configures an injector with a DI token, which that
  injector uses to provide the concrete, runtime version of a dependency value.
  The injector relies on the provider configuration
---

# Dependency Providers

 You must configure an injector with a provider, or it won't know how to create the dependency.

### The [`Provider`](https://angular.io/api/core/Provider) object literal \(\[{ provide: Logger, useClass: Logger }\]\) <a id="the-provider-object-literal"></a>

The expanded provider configuration is an object literal with two properties.

* The `provide` property holds the [token](https://angular.io/guide/dependency-injection#token) that serves as the key for both locating a dependency value and configuring the injector.
* The second property is a provider definition object, which tells the injector how to create the dependency value. The provider-definition key can be `useClass`, as in the example. It can also be `useExisting`, `useValue`, or `useFactory`. Each of these keys provides a different type of dependency, as discussed below.

## Alternative class providers

 Different classes can provide the same service. 

\[{ provide: Logger, useClass: BetterLogger }\]

```typescript
@Injectable()
export class EvenBetterLogger extends Logger {
  constructor(private userService: UserService) { super(); }

  log(message: string) {
    let name = this.userService.user.name;
    super.log(`Message to ${name}: ${message}`);
  }
}
```

## Value providers \(\[{ provide: Logger, useValue: silentLogger }\]\)

```typescript
// An object in the shape of the logger service
export function SilentLoggerFn() {}

const silentLogger = {
  logs: ['Silent logger says "Shhhhh!". Provided via "useValue"'],
  log: SilentLoggerFn
};
```

#### Non-class dependencies <a id="non-class-dependencies"></a>

 Not all dependencies are classes. Sometimes you want to inject a string, function, or object.

```typescript
export const HERO_DI_CONFIG: AppConfig = {
  apiEndpoint: 'api.heroes.com',
  title: 'Dependency Injection'
};
```

 **TypeScript interfaces are not valid tokens**

{% code-tabs %}
{% code-tabs-item title="Solution 1" %}
```typescript
providers: [
  UserService,
  { provide: APP_CONFIG, useValue: HERO_DI_CONFIG }
],
```
{% endcode-tabs-item %}

{% code-tabs-item title="Solution 2" %}
```typescript
import { InjectionToken } from '@angular/core';

export const APP_CONFIG = new InjectionToken<AppConfig>('app.config');
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 **For solution 2,** you can inject the configuration object into any constructor that needs it, with the help of an `@`[`Inject`](https://angular.io/api/core/Inject)`()` parameter decorator.

```typescript
constructor(@Inject(APP_CONFIG) config: AppConfig) {
  this.title = config.title;
}
```

## Factory providers

 Sometimes you need to create a dependent value dynamically, based on information you won't have until run time. 

```typescript
let heroServiceFactory = (logger: Logger, userService: UserService) => {
  return new HeroService(logger, userService.user.isAuthorized);
};
```

```typescript
export let heroServiceProvider =
  { provide: HeroService,
    useFactory: heroServiceFactory,
    deps: [Logger, UserService]
  };
```

## Predefined tokens and multiple providers

 Angular provides a number of built-in injection-token constants that you can use to customize the behavior of various systems.

A provider object can associate any of these injection tokens with one or more callback functions that take app-specific initialization actions.

* [PLATFORM\_INITIALIZER](https://angular.io/api/core/PLATFORM_INITIALIZER): Callback is invoked when a platform is initialized.
* [APP\_BOOTSTRAP\_LISTENER](https://angular.io/api/core/APP_BOOTSTRAP_LISTENER): Callback is invoked for each component that is bootstrapped. The handler function receives the ComponentRef instance of the bootstrapped component.
* [APP\_INITIALIZER](https://angular.io/api/core/APP_INITIALIZER): Callback is invoked before an app is initialized. All registered initializers can optionally return a Promise. All initializer functions that return Promises must be resolved before the application is bootstrapped. If one of the initializers fails to resolves, the application is not bootstrapped.

 The provider object can have a third option, `multi: true`, which you can use with [`APP_INITIALIZER`](https://angular.io/api/core/APP_INITIALIZER) to register multiple handlers for the provide event.

```typescript
export const APP_TOKENS = [
 { provide: PLATFORM_INITIALIZER, useFactory: platformInitialized, multi: true    },
 { provide: APP_INITIALIZER, useFactory: delayBootstrapping, multi: true },
 { provide: APP_BOOTSTRAP_LISTENER, useFactory: appBootstrapped, multi: true },
];
```

## Tree-shakable providers

Tree shaking refers to a compiler option that removes code from the final bundle if that code not referenced in an application. When providers are tree-shakable, the Angular compiler removes the associated services from the final output when it determines that they are not used in your application. This significantly reduces the size of your bundles.



