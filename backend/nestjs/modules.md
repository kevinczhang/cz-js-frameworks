---
description: A module is a class annotated with a @Module() decorator.
---

# Modules

The @Module\(\) decorator provides metadata that Nest makes use of to organize the application structure. 

 Each application has at least one module, a **root module**. The root module is the starting point Nest uses to build the **application graph** - the internal data structure Nest uses to resolve module and provider relationships and dependencies.

The `@Module()` decorator takes a single object whose properties describe the module:

| `providers` | the providers that will be instantiated by the Nest injector and that may be shared at least across this module |
| :--- | :--- |
| `controllers` | the set of controllers defined in this module which have to be instantiated |
| `imports` | the list of imported modules that export the providers which are required in this module |
| `exports` | the subset of `providers` that are provided by this module and should be available in other modules which import this module |

## **Feature modules**

A feature module simply organizes code relevant for a specific feature, keeping code organized and establishing clear boundaries. This helps us manage complexity and develop with [SOLID](https://en.wikipedia.org/wiki/SOLID) principles, especially as the size of the application and/or team grow.

```javascript
import { Module } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {}
```

```javascript
import { Module } from '@nestjs/common';
import { CatsModule } from './cats/cats.module';

@Module({
  imports: [CatsModule],
})
export class AppModule {}
```

## **Shared modules**

 In Nest, modules are **singletons** by default, and thus you can share the same instance of any provider between multiple modules effortlessly.

Let's imagine that we want to share an instance of the `CatsService` between several other modules. In order to do that, we first need to **export** the `CatsService` provider by adding it to the module's `exports` array**.**

## **Global modules**

 When you want to provide a set of providers which should be available everywhere out-of-the-box \(e.g., helpers, database connections, etc.\), make the module **global** with the `@Global()` decorator.

```javascript
import { Module, Global } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Global()
@Module({
  controllers: [CatsController],
  providers: [CatsService],
  exports: [CatsService],
})
export class CatsModule {}
```

 The `@Global()` decorator makes the module global-scoped. Global modules should be registered **only once**, generally by the root or core module. In the above example, the `CatsService` provider will be ubiquitous, and modules that wish to inject the service will not need to import the `CatsModule` in their imports array.



