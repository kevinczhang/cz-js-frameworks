# Routing Test

## Test setup

To test routing we need a few components and a route configuration:

```typescript
import {Component} from "@angular/core";
import {Routes} from "@angular/router";

@Component({
  template: `Search`
})
export class SearchComponent {
}

@Component({
  template: `Home`
})
export class HomeComponent {
}

@Component({
  template: `<router-outlet></router-outlet>`
})
export class AppComponent {
}

export const routes: Routes = [
  {path: '', redirectTo: 'home', pathMatch: 'full'},
  {path: 'home', component: HomeComponent},
  {path: 'search', component: SearchComponent}
];
```

## Router setup

Normally to setup routing in an Angular application we import the `RouterModule` and _provide_ the routes to the `NgModule` with `RouterModule.withRoutes(routes)`.

However when testing routing we use the `RouterTestingModule` instead. This modules sets up the router with a _spy_ implementation of the _Location Strategy_ that doesn’t actually change the URL.

We also need to get the injected `Router` and `Location` so we can use them in the test specs.

```typescript
describe('Router: App', () => {

  let location: Location;
  let router: Router;
  let fixture;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [RouterTestingModule.withRoutes(routes)], (1)
      declarations: [
        HomeComponent,
        SearchComponent,
        AppComponent
      ]
    });

    router = TestBed.get(Router); (2)
    location = TestBed.get(Location); (3)

    fixture = TestBed.createComponent(AppComponent); (4)
    router.initialNavigation(); (5)
  });
});
```

1. &#x20;We import our `RouterTestingModule` with our routes.
2. &#x20;We grab a reference to the injected `Router`.
3. &#x20;We grab a reference to the injected `Location`.
4. &#x20;We ask the test bed to create an instance of our root `AppComponent`. We don’t need this reference in our test specs but we do need to create the root component with the `router-outlet` so the router has somewhere to insert components.
5. This sets up the location change listener and performs the initial navigation.

## Testing routing

&#x20;In our configuration we’ve set it so if you land on the root _empty_ url you will be redirected to `/home`, lets add a test spec for this:

```typescript
it('navigate to "" redirects you to /home', fakeAsync(() => { (1)
  router.navigate(['']); (2)
  tick(); (3)
  expect(location.path()).toBe('/home'); (4)
}));
```

1. &#x20;Routing is an asynchronous activity so we use one of the asynchronous testing methods at our disposal, in this case the `fakeAsync` method.
2. We trigger the router to navigate to the empty path.
3. We wait for all pending promises to be resolved.
4. &#x20;We can then inspect the _path_ our application should be at with `location.path()`

Lets also add a test spec for navigating to the search route, like so:

```typescript
it('navigate to "search" takes you to /search', fakeAsync(() => {
  router.navigate(['search']);
  tick();
  expect(location.path()).toBe('/search');
}));
```

