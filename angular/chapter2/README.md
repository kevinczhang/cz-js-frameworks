# Components & Templates

## The safe navigation operator \( ?. \) and null property paths

### **safe navigation operator \(**`?.`**\)**

The Angular **safe navigation operator \(**`?.`**\)** is a fluent and convenient way to guard against null and undefined values in property paths. Here it is, protecting against a view render failure if the `currentHero`is null.

```typescript
<!-- No hero, no problem! -->
The null hero's name is {{nullHero?.name}}
```

### The non-null assertion operator \( ! \)

As of Typescript 2.0, you can enforce [strict null checking](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html) with the `--strictNullChecks` flag. TypeScript then ensures that no variable is _unintentionally_ null or undefined.

The _Angular_ **non-null assertion operator \(**`!`**\)** serves the same purpose in an Angular template.

```markup
<!--No hero, no text -->
<div *ngIf="hero">
  The hero's name is {{hero!.name}}
</div>
```

Unlike the [_safe navigation operator_](https://angular.io/guide/template-syntax#safe-navigation-operator), the **non-null assertion operator** does not guard against null or undefined. Rather it tells the TypeScript type checker to suspend strict null checks for a specific property expression. You'll need this template operator when you turn on strict null checks. It's optional otherwise.

## The `$any` type cast function \(`$any( <expression> )`\)

Sometimes a binding expression will be reported as a type error and it is not possible or difficult to fully specify the type.

```markup
<!-- Accessing an undeclared member -->
<div>
  The hero's marker is {{$any(hero).marker}}
</div>
```

## Special selectors for component styling

### :host

Use the `:`[`host`](https://angular.io/api/core/Directive#host) pseudo-class selector to target styles in the element that _hosts_ the component \(as opposed to targeting elements _inside_ the component's template\).

```css
:host(.active) {
  border-width: 3px;
}
```

### :host-context

Sometimes it's useful to apply styles based on some condition _outside_ of a component's view. The `:host-context()` selector looks for a CSS class in any ancestor of the component host element, up to the document root. The `:host-context()` selector is useful when combined with another selector.

The following example applies a `background-color` style to all `<h2>` elements _inside_ the component, only if some ancestor element has the CSS class `theme-light`.

```css
:host-context(.theme-light) h2 {
  background-color: #eef;
}
```

##  Dynamic Component example

[https://angular.io/guide/dynamic-component-loader](https://angular.io/guide/dynamic-component-loader)

