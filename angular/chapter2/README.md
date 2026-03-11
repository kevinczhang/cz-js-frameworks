# Components

Components are the main building block for Angular applications. Each component consists of:

* An HTML template that declares what renders on the page
* A TypeScript class that defines behavior
* A CSS selector that defines how the component is used in a template
* Optionally, CSS styles applied to the template

```typescript
app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'angular-tutorial';
}
```

## The safe navigation operator ( ?. ) and null property paths

### **safe navigation operator (**`?.`**)**

The Angular **safe navigation operator (**`?.`**)** is a fluent and convenient way to guard against null and undefined values in property paths. Here it is, protecting against a view render failure if the `currentHero`is null.

```typescript
<!-- No hero, no problem! -->
The null hero's name is {{nullHero?.name}}
```

### The non-null assertion operator ( ! )

As of Typescript 2.0, you can enforce [strict null checking](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html) with the `--strictNullChecks` flag. TypeScript then ensures that no variable is _unintentionally_ null or undefined.

The _Angular_ **non-null assertion operator (**`!`**)** serves the same purpose in an Angular template.

```markup
<!--No hero, no text -->
<div *ngIf="hero">
  The hero's name is {{hero!.name}}
</div>
```

Unlike the [_safe navigation operator_](https://angular.io/guide/template-syntax#safe-navigation-operator), the **non-null assertion operator** does not guard against null or undefined. Rather it tells the TypeScript type checker to suspend strict null checks for a specific property expression. You'll need this template operator when you turn on strict null checks. It's optional otherwise.

## The `$any` type cast function (`$any( <expression> )`)

Sometimes a binding expression will be reported as a type error and it is not possible or difficult to fully specify the type.

```markup
<!-- Accessing an undeclared member -->
<div>
  The hero's marker is {{$any(hero).marker}}
</div>
```

##

## Dynamic Component example

[https://angular.io/guide/dynamic-component-loader](https://angular.io/guide/dynamic-component-loader)
