# Lazy loading

## Basics <a href="#lazy-loading-basics" id="lazy-loading-basics"></a>

To lazy load Angular modules, use `loadChildren` (instead of `component`) in your `AppRoutingModule` `routes` configuration as follows.

```typescript
const routes: Routes = [
  {
    path: 'items',
    loadChildren: () => import('./items/items.module').then(m => m.ItemsModule)
  }
];
```

In the lazy-loaded module's routing module, add a route for the component.

```typescript
const routes: Routes = [
  {
    path: '',
    component: ItemsComponent
  }
];
```

### `forRoot()` and `forChild()` <a href="#forroot-and-forchild" id="forroot-and-forchild"></a>

You might have noticed that the Angular CLI adds `RouterModule.forRoot(routes)` to the `AppRoutingModule` `imports` array. This lets Angular know that the `AppRoutingModule` is a routing module and `forRoot()` specifies that this is the root routing module. It configures all the routes you pass to it, gives you access to the router directives, and registers the [`Router`](https://angular.io/api/router/Router) service. Use `forRoot()` only once in the application, inside the `AppRoutingModule`.

The Angular CLI also adds `RouterModule.forChild(routes)` to feature routing modules. This way, Angular knows that the route list is only responsible for providing extra routes and is intended for feature modules. You can use `forChild()` in multiple modules.

The `forRoot()` method takes care of the _global_ injector configuration for the Router. The `forChild()` method has no injector configuration. It uses directives such as [`RouterOutlet`](https://angular.io/api/router/RouterOutlet) and [`RouterLink`](https://angular.io/api/router/RouterLink).

## Preloading <a href="#preloading" id="preloading"></a>

Preloading improves UX by loading parts of your application **in the background**. You can preload modules or component data.

To enable preloading of all lazy loaded modules, import the [`PreloadAllModules`](https://angular.io/api/router/PreloadAllModules) token from the Angular `router`.

```typescript
import { PreloadAllModules } from '@angular/router';

RouterModule.forRoot(
  appRoutes,
  {
    preloadingStrategy: PreloadAllModules
  }
)
```

### Preloading component data

To preload component data, use a `resolver`. Resolvers improve UX by blocking the page load until all necessary data is available to fully display the page.

#### **Resolvers**

```typescript
import { Resolve } from '@angular/router';

…

/* An interface that represents your data model */
export interface Crisis {
  id: number;
  name: string;
}

export class CrisisDetailResolverService implements Resolve<Crisis> {
  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Crisis> {
    // your logic goes here
  }
}yy
```

Import this resolver into your module's routing module.

```typescript
import { CrisisDetailResolverService } from './crisis-detail-resolver.service';

{
  path: '/your-path',
  component: YourComponent,
  resolve: {
    crisis: CrisisDetailResolverService
  }
}

```

Use the injected instance of the [`ActivatedRoute`](https://angular.io/api/router/ActivatedRoute) class to access `data` associated with a given route.

```typescript
import { ActivatedRoute } from '@angular/router';

@Component({ … })
class YourComponent {
  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    this.route.data
      .subscribe(data => {
        const crisis: Crisis = data.crisis;
        // …
      });
  }
}ty
```
