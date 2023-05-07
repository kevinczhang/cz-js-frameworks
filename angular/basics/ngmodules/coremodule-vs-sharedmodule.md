# CoreModule vs SharedModule

## Core module or Core feature module <a href="#e031" id="e031"></a>

The core module is a module that is **only imported once in the AppModule** and never again in the other modules. To ensure your module is only imported one time (if you are working on a team of sneaky members) , you can put this code in the class constructor that will prevent the module from being imported twice:

```typescript
export class CoreModule {
  constructor(@Optional() @SkipSelf() parentModule: CoreModule) {
    throwIfAlreadyLoaded(parentModule, 'CoreModule');
  }

  static forRoot(): ModuleWithProviders<CoreModule> {
    return {
      ngModule: CoreModule
    };
  }
}
```

&#x20;So why do we need to import that famous module only once ? The reason behind this is that we want everything that’s inside the core module to be a **Singleton** !!! And this is very important if you need your components/services to have only one instance. Some usage examples are the profile service or the **header or footer** components.

## Shared module or Shared feature module <a href="#14be" id="14be"></a>

The SharedModule in contradiction with the CoreModule is imported in every feature module that needs some shared components.

It’s recommended to **avoid having services** in the SharedModule because you will end up with a lot of instances of that service.

The SharedModule is the perfect place for importing and exporting back your UI Modules or components that are used a lot in your application. This will make your code more readable and maintainable, some good examples of the SharedModule use case are importing and exporting **Angular Material modules and/or the Flex Layout Module**. By doing this, you only have to import the SharedModule in your feature Module and voila !! All your imported Angular Material Modules/components are available and the import bloc on top of your file is much much smaller.
