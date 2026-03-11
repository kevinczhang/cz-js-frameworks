---
description: >-
  Angular Test Bed (ATB) is a higher level Angular Only testing framework that
  allows us to easily test behaviours that depend on the Angular Framework.
---

# Angular Test Bed

## &#x20;Configuring

```typescript
/* tslint:disable:no-unused-variable */
import {TestBed, ComponentFixture} from '@angular/core/testing';
import {LoginComponent} from './login.component';
import {AuthService} from "./auth.service";

describe('Component: Login', () => {

  let component: LoginComponent;
  let fixture: ComponentFixture<LoginComponent>; (1)
  let authService: AuthService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [LoginComponent],
      providers: [AuthService]
    });

    // create component and test fixture
    fixture = TestBed.createComponent(LoginComponent); (2)

    // get test component from the fixture
    component = fixture.componentInstance; (3)

    // UserService provided to the TestBed
    authService = TestBed.get(AuthService); (4)

  });
});
```

In the `beforeEach` function for our test suite we _configure_ a testing module using the `TestBed` class. This creates a test _Angular Module_ which we can use to instantiate components, perform dependency injection and so on.

## Fixtures and DI

1. &#x20;A `fixture` is a wrapper for a component _and_ it’s template.
2. &#x20;We create an instance of a component fixture through the `TestBed`, this injects the `AuthService`into the component constructor.
3. &#x20;We can find the actual _component_ from the `componentInstance` on the `fixture`.
4. &#x20;We can get resolve dependencies using the TestBed injector by using the `get` function.

## Test specs

```typescript
it('canLogin returns false when the user is not authenticated', () => {
  spyOn(authService, 'isAuthenticated').and.returnValue(false);
  expect(component.needsLogin()).toBeTruthy();
  expect(authService.isAuthenticated).toHaveBeenCalled();
});

it('canLogin returns false when the user is not authenticated', () => {
  spyOn(authService, 'isAuthenticated').and.returnValue(true);
  expect(component.needsLogin()).toBeFalsy();
  expect(authService.isAuthenticated).toHaveBeenCalled();
});
```
