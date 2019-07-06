---
description: >-
  Angular templates are dynamic. When Angular renders them, it transforms the
  DOM according to the instructions given by directives. A directive is a class
  with a @Directive() decorator.
---

# Directives

## Directives overview

There are three kinds of directives in Angular:

1. Components—directives with a template.
2. Structural directives—change the DOM layout by adding and removing DOM elements.
3. Attribute directives—change the appearance or behavior of an element, component, or another directive.

## Attribute directive

An attribute directive minimally requires building a controller class annotated with `@`[`Directive`](https://angular.io/api/core/Directive), which specifies the selector that identifies the attribute.

```bash
ng generate directive highlight
```

{% code-tabs %}
{% code-tabs-item title="app/app.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  color: string;
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="app/app.component.html" %}
```markup
<h1>My First Attribute Directive</h1>

<h4>Pick a highlight color</h4>
<div>
  <input type="radio" name="colors" (click)="color='lightgreen'">Green
  <input type="radio" name="colors" (click)="color='yellow'">Yellow
  <input type="radio" name="colors" (click)="color='cyan'">Cyan
</div>
<p [appHighlight]="color">Highlight me!</p>

<p [appHighlight]="color" defaultColor="violet">
  Highlight me too!
</p>
```
{% endcode-tabs-item %}

{% code-tabs-item title="app/highlight.directive.ts" %}
```typescript
/* tslint:disable:member-ordering */
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {

  constructor(private el: ElementRef) { }

  @Input() defaultColor: string;

  @Input('appHighlight') highlightColor: string;

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.highlightColor || this.defaultColor || 'red');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="app/app.module.ts" %}
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';
import { HighlightDirective } from './highlight.directive';

@NgModule({
  imports: [ BrowserModule ],
  declarations: [
    AppComponent,
    HighlightDirective
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

It's the brackets \(`[]`\) that make it an attribute selector.

### Built-in _attribute_ directives

* [`NgClass`](https://angular.io/guide/template-syntax#ngClass) - add and remove a set of CSS classes
* [`NgStyle`](https://angular.io/guide/template-syntax#ngStyle) - add and remove a set of HTML styles
* [`NgModel`](https://angular.io/guide/template-syntax#ngModel) - two-way data binding to an HTML form element \(FormsModule is required to use ngModel\)

## Structural Directives

Structural directives are responsible for HTML layout. They shape or reshape the DOM's _structure_, typically by adding, removing, or manipulating elements. Structural directives are easy to recognize. An asterisk \(\*\) precedes the directive attribute name.

### The asterisk \(\*\) prefix  <a id="the-asterisk--prefix"></a>

Internally, Angular translates the `*`[`ngIf`](https://angular.io/api/common/NgIf) _attribute_ into a `<ng-template>` _element_, wrapped around the host element, like this.

```markup
<ng-template [ngIf]="hero">
  <div class="name">{{hero.name}}</div>
</ng-template>
```

#### One structural directive per host element.  You may apply only one _structural_ directive to an element.  <a id="one-structural-directive-per-host-element"></a>

### The _&lt;ng-template&gt;_

The &lt;ng-template&gt; is an Angular element for rendering HTML. It is never displayed directly. In fact, before rendering the view, Angular _replaces_ the `<ng-template>` and its contents with a comment.

### Group sibling elements with &lt;ng-container&gt;  <a id="group-sibling-elements-with-ng-container"></a>

The Angular `<ng-container>` is a grouping element that doesn't interfere with styles or layout because Angular _doesn't put it in the DOM_. \_\_ The `<ng-container>` is a syntax element recognized by the Angular parser. It's not a directive, component, class, or interface. It's more like the curly braces in a JavaScript `if`-block. Without those braces, JavaScript would only execute the first statement when you intend to conditionally execute all of them as a single block. The `<ng-container>` satisfies a similar need in Angular templates.

{% code-tabs %}
{% code-tabs-item title="ngif-ngcontainer" %}
```markup
<p>
  I turned the corner
  <ng-container *ngIf="hero">
    and saw {{hero.name}}. I waved
  </ng-container>
  and continued on my way.
</p>
```
{% endcode-tabs-item %}

{% code-tabs-item title="select-ngcontainer" %}
```markup
<div>
  Pick your favorite hero
  (<label><input type="checkbox" checked (change)="showSad = !showSad">show sad</label>)
</div>
<select [(ngModel)]="hero">
  <ng-container *ngFor="let h of heroes">
    <ng-container *ngIf="showSad || h.emotion !== 'sad'">
      <option [ngValue]="h">{{h.name}} ({{h.emotion}})</option>
    </ng-container>
  </ng-container>
</select>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Built-in _structural_ directives

* [`NgIf`](https://angular.io/guide/template-syntax#ngIf) - conditionally add or remove an element from the DOM
* [`NgSwitch`](https://angular.io/guide/template-syntax#ngSwitch) - a set of directives that switch among alternative views
* [`NgForOf`](https://angular.io/guide/template-syntax#ngFor) - repeat a template for each item in a list

```typescript
<div *ngIf="hero" class="name">{{hero.name}}</div>

<ul>
  <li *ngFor="let hero of heroes">{{hero.name}}</li>
</ul>

<div [ngSwitch]="hero?.emotion">
  <app-happy-hero    *ngSwitchCase="'happy'"    [hero]="hero"></app-happy-hero>
  <app-sad-hero      *ngSwitchCase="'sad'"      [hero]="hero"></app-sad-hero>
  <app-confused-hero *ngSwitchCase="'app-confused'" [hero]="hero"></app-confused-hero>
  <app-unknown-hero  *ngSwitchDefault           [hero]="hero"></app-unknown-hero>
</div>
```

### Write a structural directive  <a id="write-a-structural-directive"></a>

In this section, you write an `UnlessDirective` structural directive that does the opposite of [`NgIf`](https://angular.io/api/common/NgIf)`.`

#### _TemplateRef_ and _ViewContainerRef_  <a id="templateref-and-viewcontainerref"></a>

A simple structural directive like this one creates an [_embedded view_](https://angular.io/api/core/EmbeddedViewRef) from the Angular-generated `<ng-template>` and inserts that view in a [_view container_](https://angular.io/api/core/ViewContainerRef) adjacent to the directive's original `<p>` host element.

You'll acquire the `<ng-template>` contents with a [`TemplateRef`](https://angular.io/api/core/TemplateRef) and access the _view container_ through a[`ViewContainerRef`](https://angular.io/api/core/ViewContainerRef).

{% code-tabs %}
{% code-tabs-item title="unless.directive.ts" %}
```typescript
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

/**
 * Add the template content to the DOM unless the condition is true.
 */
@Directive({ selector: '[appUnless]'})
export class UnlessDirective {
  private hasView = false;

  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef) { }

  @Input() set appUnless(condition: boolean) {
    if (!condition && !this.hasView) {
      this.viewContainer.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      this.viewContainer.clear();
      this.hasView = false;
    }
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="app.component.html" %}
```markup
<p *appUnless="condition" class="unless a">
  (A) This paragraph is displayed because the condition is false.
</p>

<p *appUnless="!condition" class="unless b">
  (B) Although the condition is true,
  this paragraph is displayed because appUnless is set to false.
</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

