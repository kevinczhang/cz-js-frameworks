# Intro to services and DI

_Service_ is a broad category encompassing any value, function, or feature that an app needs.

Ideally, a component's job is to enable the user experience and nothing more. A component should present properties and methods for data binding, in order to mediate between the view and the application logic.

A component can delegate certain tasks to services, such as fetching data from the server, validating user input, or logging directly to the console.

## Dependency injection \(DI\)

To define a class as a service in Angular, use the **@Injectable\(\)** decorator to provide the metadata that allows Angular to inject it into a component as a dependency.

* The **injecto**r is the main mechanism. Angular creates an application-wide injector for you during the bootstrap process, and additional injectors as needed. You don't have to create injectors.
* An injector creates dependencies, and maintains a container of dependency instances that it reuses if possible.
* A **provider** is an object that tells an injector how to obtain or create a dependency.

For any dependency that you need in your app, you must register a provider with the app's injector, so that the injector can use the provider to create new instances. For a service, the provider is typically the service class itself.

## Providing services

You must register at least one _provider_ of any service you are going to use. By default, the Angular CLI command ng generate service **registers a provider with the root injector** for your service by including provider metadata in the @Injectable\(\) decorator.

```javascript
@Injectable({
 providedIn: 'root',
})
```

*  When you provide the service at the root level, Angular creates a single, shared instance of `HeroService` and injects it into any class that asks for it. Registering the provider in the `@`[`Injectable`](https://angular.io/api/core/Injectable)`()` metadata also allows Angular to optimize an app by removing the service from the compiled app if it isn't used.
*  When you register a provider with a [specific NgModule](https://angular.io/guide/architecture-modules), the same instance of a service is available to all components in that NgModule. To register at this level, use the `providers` property of the `@`[`NgModule`](https://angular.io/api/core/NgModule)`()` decorator.
*  When you register a provider at the component level, you get a new instance of the service with each new instance of that component. At the component level, register a service provider in the `providers` property of the `@`[`Component`](https://angular.io/api/core/Component)`()` metadata.

