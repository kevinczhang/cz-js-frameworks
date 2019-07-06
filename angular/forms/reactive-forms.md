---
description: >-
  Reactive forms provide a model-driven approach to handling form inputs whose
  values change over time.
---

# Reactive Forms

### Introduction <a id="introduction-to-reactive-forms"></a>

Reactive forms use an explicit and immutable approach to managing the state of a form at a given point in time. Each change to the form state returns a new state, which maintains the integrity of the model between changes. 

Reactive forms are built around observable streams, where form inputs and values are provided as streams of input values, which can be accessed synchronously.

1.  To use reactive forms, import [`ReactiveFormsModule`](https://angular.io/api/forms/ReactiveFormsModule) from the `@angular/forms` package and add it to your NgModule's [`imports`](https://angular.io/api/core/NgModule#imports) array.
2.  To register a single form control, import the [`FormControl`](https://angular.io/api/forms/FormControl) class into your component and create a new instance of the form control to save as a class property.
3.  Update the template with the form control using the `formControl` binding provided by [`FormControlDirective`](https://angular.io/api/forms/FormControlDirective) included in [`ReactiveFormsModule`](https://angular.io/api/forms/ReactiveFormsModule).
4.   A form control instance provides a `setValue()` method that updates the value of the form control and validates the structure of the value provided against the control's structure. 

### Grouping form controls <a id="grouping-form-controls"></a>

 Just as a form control instance gives you control over a single input field, a form group instance tracks the form state of a group of form control instances \(for example, a form\). Each control in a form group instance is tracked by name when creating the form group. 

 The [`FormGroup`](https://angular.io/api/forms/FormGroup)directive listens for the `submit` event emitted by the `form` element and emits an `ngSubmit` event that you can bind to a callback function.

{% hint style="info" %}
 **Note:** Display the value for the form group instance in the component template using the `value` property and [`JsonPipe`](https://angular.io/api/common/JsonPipe).
{% endhint %}

### Partial model updates <a id="partial-model-updates"></a>

There are two ways to update the model value:

* Use the `setValue()` method to set a new value for an individual control. The `setValue()` method strictly adheres to the structure of the form group and replaces the entire value for the control.
* Use the `patchValue()` method to replace any properties defined in the object that have changed in the form model.

The strict checks of the `setValue()` method help catch nesting errors in complex forms, while `patchValue()` fails silently on those errors.

```typescript
updateProfile() {
  this.profileForm.patchValue({
    firstName: 'Nancy',
    address: {
      street: '123 Drew Street'
    }
  });
}
```

### Generating form controls with FormBuilder <a id="generating-form-controls-with-formbuilder"></a>

1.  Import the [`FormBuilder`](https://angular.io/api/forms/FormBuilder) class from the `@angular/forms` package.
2.  The [`FormBuilder`](https://angular.io/api/forms/FormBuilder) service is an injectable provider that is provided with the reactive forms module. Inject this dependency by adding it to the component constructor.
3.  The [`FormBuilder`](https://angular.io/api/forms/FormBuilder) service has three methods: [`control()`](https://angular.io/api/forms/FormBuilder#control), [`group()`](https://angular.io/api/forms/FormBuilder#group), and [`array()`](https://angular.io/api/forms/FormBuilder#array). These are factory methods for generating instances in your component classes including form controls, form groups, and form arrays.
4. Import the [`Validators`](https://angular.io/api/forms/Validators) class from the `@angular/forms` package.

{% hint style="info" %}
 **Note:** You can define the control with just the initial value, but if your controls need sync or async validation, add sync and async validators as the second and third items in the array.
{% endhint %}

### Dynamic controls using form arrays <a id="dynamic-controls-using-form-arrays"></a>

 [`FormArray`](https://angular.io/api/forms/FormArray) is an alternative to [`FormGroup`](https://angular.io/api/forms/FormGroup) for managing any number of unnamed controls. As with form group instances, you can dynamically insert and remove controls from form array instances, and the form array instance value and validation status is calculated from its child controls.

1.  Import the [`FormArray`](https://angular.io/api/forms/FormArray) class from `@angular/forms` to use for type information. The [`FormBuilder`](https://angular.io/api/forms/FormBuilder) service is ready to create a [`FormArray`](https://angular.io/api/forms/FormArray) instance.
2. Use the [`FormBuilder.array()`](https://angular.io/api/forms/FormBuilder#array) method to define the array, and the [`FormBuilder.control()`](https://angular.io/api/forms/FormBuilder#control) method to populate the array with an initial control.
3.  The form array instance represents an undefined number of controls in an array. It's convenient to access a control through a getter, and this approach is easy to repeat for additional controls.
4.  Similar to the [`formGroupName`](https://angular.io/api/forms/FormGroupName) input provided by `FormGroupNameDirective`, [`formArrayName`](https://angular.io/api/forms/FormArrayName) binds communication from the form array instance to the template with `FormArrayNameDirective`.

{% hint style="info" %}
 **Note:** Because the returned control is of the type [`AbstractControl`](https://angular.io/api/forms/AbstractControl), you need to provide an explicit type to access the method syntax for the form array instance.
{% endhint %}

```markup
<div formArrayName="aliases">
  <h3>Aliases</h3> <button (click)="addAlias()">Add Alias</button>

  <div *ngFor="let address of aliases.controls; let i=index">
    <!-- The repeated alias template -->
    <label>
      Alias:
      <input type="text" [formControlName]="i">
    </label>
  </div>
</div>
```

#### Reactive forms API <a id="reactive-forms-api"></a>

**Classes**

| Class | Description |
| :--- | :--- |
| [`AbstractControl`](https://angular.io/api/forms/AbstractControl) | The abstract base class for the concrete form control classes [`FormControl`](https://angular.io/api/forms/FormControl), [`FormGroup`](https://angular.io/api/forms/FormGroup), and [`FormArray`](https://angular.io/api/forms/FormArray). It provides their common behaviors and properties. |
| [`FormControl`](https://angular.io/api/forms/FormControl) | Manages the value and validity status of an individual form control. It corresponds to an HTML form control such as `<input>` or `<select>`. |
| [`FormGroup`](https://angular.io/api/forms/FormGroup) | Manages the value and validity state of a group of [`AbstractControl`](https://angular.io/api/forms/AbstractControl)instances. The group's properties include its child controls. The top-level form in your component is [`FormGroup`](https://angular.io/api/forms/FormGroup). |
| [`FormArray`](https://angular.io/api/forms/FormArray) | Manages the value and validity state of a numerically indexed array of [`AbstractControl`](https://angular.io/api/forms/AbstractControl) instances. |
| [`FormBuilder`](https://angular.io/api/forms/FormBuilder) | An injectable service that provides factory methods for creating control instances. |

**Directives**

| Directive | Description |
| :--- | :--- |
| [`FormControlDirective`](https://angular.io/api/forms/FormControlDirective) | Syncs a standalone [`FormControl`](https://angular.io/api/forms/FormControl) instance to a form control element. |
| [`FormControlName`](https://angular.io/api/forms/FormControlName) | Syncs [`FormControl`](https://angular.io/api/forms/FormControl) in an existing [`FormGroup`](https://angular.io/api/forms/FormGroup) instance to a form control element by name. |
| [`FormGroupDirective`](https://angular.io/api/forms/FormGroupDirective) | Syncs an existing [`FormGroup`](https://angular.io/api/forms/FormGroup) instance to a DOM element. |
| [`FormGroupName`](https://angular.io/api/forms/FormGroupName) | Syncs a nested [`FormGroup`](https://angular.io/api/forms/FormGroup) instance to a DOM element. |
| [`FormArrayName`](https://angular.io/api/forms/FormArrayName) | Syncs a nested [`FormArray`](https://angular.io/api/forms/FormArray) instance to a DOM element. |



