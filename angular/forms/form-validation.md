---
description: >-
  Improve overall data quality by validating user input for accuracy and
  completeness.
---

# Form Validation

## Template-driven validation

 Every time the value of a form control changes, Angular runs validation and generates either a list of validation errors, which results in an INVALID status, or null, which results in a VALID status.

```markup
<input id="name" name="name" class="form-control"
      required minlength="4" appForbiddenName="bob"
      [(ngModel)]="hero.name" #name="ngModel" >

<div *ngIf="name.invalid && (name.dirty || name.touched)"
    class="alert alert-danger">

  <div *ngIf="name.errors.required">
    Name is required.
  </div>
  <div *ngIf="name.errors.minlength">
    Name must be at least 4 characters long.
  </div>
  <div *ngIf="name.errors.forbiddenName">
    Name cannot be Bob.
  </div>

</div>
```

{% hint style="info" %}
**Why check dirty and touched?**

You may not want your application to display errors before the user has a chance to edit the form. The checks for `dirty` and `touched` prevent errors from showing until the user does one of two things: changes the value, turning the control dirty; or blurs the form control element, setting the control to touched.
{% endhint %}

## Reactive form validation

There are two types of validator functions: sync validators and async validators.

* **Sync validators**: functions that take a control instance and immediately return either a set of validation errors or `null`. You can pass these in as the second argument when you instantiate a [`FormControl`](https://angular.io/api/forms/FormControl).
* **Async validators**: functions that take a control instance and return a Promise or Observable that later emits a set of validation errors or `null`. You can pass these in as the third argument when you instantiate a [`FormControl`](https://angular.io/api/forms/FormControl).

## Custom validators

{% code-tabs %}
{% code-tabs-item title="forbiddenNameValidator" %}
```typescript
/** A hero's name can't match the given regular expression */
export function forbiddenNameValidator(nameRe: RegExp): ValidatorFn {
  return (control: AbstractControl): {[key: string]: any} | null => {
    const forbidden = nameRe.test(control.value);
    return forbidden ? {'forbiddenName': {value: control.value}} : null;
  };
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="hero-form-reactive.component.ts" %}
```
this.heroForm = new FormGroup({
  'name': new FormControl(this.hero.name, [
    Validators.required,
    Validators.minLength(4),
    forbiddenNameValidator(/bob/i) // <-- Here's how you pass in the custom validator.
  ]),
  'alterEgo': new FormControl(this.hero.alterEgo),
  'power': new FormControl(this.hero.power, Validators.required)
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 The function is actually a factory that takes a regular expression to detect a _specific_ forbidden name and returns a validator function.

 The `forbiddenNameValidator` factory returns the configured validator function. That function takes an Angular control object and returns _either_ null if the control value is valid _or_ a validation error object. The validation error object typically has a property whose name is the validation key, `'forbiddenName'`, and whose value is an arbitrary dictionary of values that you could insert into an error message, `{name}`.

#### Adding to template-driven forms <a id="adding-to-template-driven-forms"></a>

 In template-driven forms, you don't have direct access to the [`FormControl`](https://angular.io/api/forms/FormControl) instance, so you can't pass the validator in like you can for reactive forms. Instead, you need to add a directive to the template.

{% code-tabs %}
{% code-tabs-item title="forbidden-name.directive.ts" %}
```typescript
@Directive({
  selector: '[appForbiddenName]',
  providers: [{provide: NG_VALIDATORS, useExisting: ForbiddenValidatorDirective, multi: true}]
})
export class ForbiddenValidatorDirective implements Validator {
  @Input('appForbiddenName') forbiddenName: string;

  validate(control: AbstractControl): {[key: string]: any} | null {
    return this.forbiddenName ? forbiddenNameValidator(new RegExp(this.forbiddenName, 'i'))(control)
                              : null;
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="hero-form-template.component.html" %}
```markup
<input id="name" name="name" class="form-control"
      required minlength="4" appForbiddenName="bob"
      [(ngModel)]="hero.name" #name="ngModel" >
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Control status CSS classes

The following classes are currently supported:

* `.ng-valid`
* `.ng-invalid`
* `.ng-pending`
* `.ng-pristine`
* `.ng-dirty`
* `.ng-untouched`
* `.ng-touched`

## Cross field validation

### Adding to reactive forms

{% code-tabs %}
{% code-tabs-item title="component" %}
```typescript
const heroForm = new FormGroup({
  'name': new FormControl(),
  'alterEgo': new FormControl(),
  'power': new FormControl()
}, { validators: identityRevealedValidator });
```
{% endcode-tabs-item %}

{% code-tabs-item title="directive" %}
```typescript
/** A hero's name can't match the hero's alter ego */
export const identityRevealedValidator: ValidatorFn = (control: FormGroup): ValidationErrors | null => {
  const name = control.get('name');
  const alterEgo = control.get('alterEgo');

  return name && alterEgo && name.value === alterEgo.value ? { 'identityRevealed': true } : null;
};
```
{% endcode-tabs-item %}

{% code-tabs-item title="html" %}
```
<div *ngIf="heroForm.errors?.identityRevealed && (heroForm.touched || heroForm.dirty)" class="cross-validation-error-message alert alert-danger">
    Name cannot match alter ego.
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Adding to template driven forms

{% code-tabs %}
{% code-tabs-item title="identity-revealed.directive.ts" %}
```typescript
@Directive({
  selector: '[appIdentityRevealed]',
  providers: [{ provide: NG_VALIDATORS, useExisting: IdentityRevealedValidatorDirective, multi: true }]
})
export class IdentityRevealedValidatorDirective implements Validator {
  validate(control: AbstractControl): ValidationErrors {
    return identityRevealedValidator(control)
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="hero-form-template.component.html" %}
```markup
<form #heroForm="ngForm" appIdentityRevealed>
<div *ngIf="heroForm.errors?.identityRevealed && (heroForm.touched || heroForm.dirty)" class="cross-validation-error-message alert alert-danger">
    Name cannot match alter ego.
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Async Validation

 Just like synchronous validators have the [`ValidatorFn`](https://angular.io/api/forms/ValidatorFn) and [`Validator`](https://angular.io/api/forms/Validator) interfaces, asynchronous validators have their own counterparts: [`AsyncValidatorFn`](https://angular.io/api/forms/AsyncValidatorFn) and [`AsyncValidator`](https://angular.io/api/forms/AsyncValidator).

They are very similar with the only difference being:

* They must return a Promise or an Observable,
* The observable returned must be finite, meaning it must complete at some point. To convert an infinite observable into a finite one, pipe the observable through a filtering operator such as `first`, `last`, `take`, or `takeUntil`.

{% hint style="info" %}
 It is important to note that the asynchronous validation happens after the synchronous validation, and is performed only if the synchronous validation is successful. 
{% endhint %}

```typescript
@Injectable({ providedIn: 'root' })
export class UniqueAlterEgoValidator implements AsyncValidator {
  constructor(private heroesService: HeroesService) {}

  validate(
    ctrl: AbstractControl
  ): Promise<ValidationErrors | null> | Observable<ValidationErrors | null> {
    return this.heroesService.isAlterEgoTaken(ctrl.value).pipe(
      map(isTaken => (isTaken ? { uniqueAlterEgo: true } : null)),
      catchError(() => null)
    );
  }
}
```

