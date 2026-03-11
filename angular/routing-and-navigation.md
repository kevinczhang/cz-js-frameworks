---
description: >-
  It can interpret a browser URL as an instruction to navigate to a
  client-generated view.
---

# Routing & Navigation

```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router'; // CLI imports router

const routes: Routes = [
  { path: 'first-component', component: FirstComponent },
  { path: 'second-component', component: SecondComponent },
  { path: '',   redirectTo: '/first-component', pathMatch: 'full' }, // redirect to `first-component`
  { path: '**', component: PageNotFoundComponent },  // Wildcard route for a 404 page
];

// configures NgModule imports and exports
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

#### Route order <a href="#route-order" id="route-order"></a>

The order of routes is important because the [`Router`](https://angular.io/api/router/Router) uses a first-match wins strategy when matching routes, so more specific routes should be placed above less specific routes. List routes with a static path first, followed by an empty path route, which matches the default route. The [wildcard route](https://angular.io/guide/router#setting-up-wildcard-routes) comes last because it matches every URL and the [`Router`](https://angular.io/api/router/Router) selects it only if no other routes match first.

### Getting route information <a href="#getting-route-information" id="getting-route-information"></a>

```typescript
import { Router, ActivatedRoute, ParamMap } from '@angular/router';

constructor(
  private route: ActivatedRoute,
) {}

ngOnInit() {
  this.route.queryParams.subscribe(params => {
    this.name = params['name'];
  });
}
```

### Nesting routes <a href="#nesting-routes" id="nesting-routes"></a>

```html
<h2>First Component</h2>

<nav>
  <ul>
    <li><a routerLink="child-a">Child A</a></li>
    <li><a routerLink="child-b">Child B</a></li>
  </ul>
</nav>

<router-outlet></router-outlet>
```

```typescript
const routes: Routes = [
  {
    path: 'first-component',
    component: FirstComponent, // this is the component with the <router-outlet> in the template
    children: [
      {
        path: 'child-a', // child route path
        component: ChildAComponent, // child route component that the router renders
      },
      {
        path: 'child-b',
        component: ChildBComponent, // another child route component that the router renders
      },
    ],
  },
];
```

