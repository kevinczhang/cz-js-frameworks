---
description: A component has a lifecycle managed by Angular.
---

# Lifecycle Hooks

Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM. A directive has the same set of lifecycle hooks.

## Lifecycle sequence

| Hook | Purpose and Timing |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngOnChanges()</code>
      </th>
      <th style="text-align:left">
        <p>Respond when Angular (re)sets data-bound input properties. The method
          receives a <a href="https://angular.io/api/core/SimpleChanges"><code>SimpleChanges</code></a> object
          of current and previous property values.</p>
        <p>Called before <code>ngOnInit()</code> and whenever one or more data-bound
          input properties change.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngOnInit()</code>
      </th>
      <th style="text-align:left">
        <p>Initialize the directive/component after Angular first displays the data-bound
          properties and sets the directive/component&apos;s input properties.</p>
        <p>Called <em>once</em>, after the <em>first</em>  <code>ngOnChanges()</code>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngDoCheck()</code>
      </th>
      <th style="text-align:left">
        <p>Detect and act upon changes that Angular can&apos;t or won&apos;t detect
          on its own.</p>
        <p>Called during every change detection run, immediately after <code>ngOnChanges()</code> and <code>ngOnInit()</code>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngAfterContentInit()</code>
      </th>
      <th style="text-align:left">
        <p>Respond after Angular projects external content into the component&apos;s
          view / the view that a directive is in.</p>
        <p>Called <em>once</em> after the first <code>ngDoCheck()</code>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><a href="https://angular.io/api/core/AfterContentChecked#ngAfterContentChecked"><code>ngAfterContentChecked()</code></a>
      </th>
      <th style="text-align:left">
        <p>Respond after Angular checks the content projected into the directive/component.</p>
        <p>Called after the <code>ngAfterContentInit()</code> and every subsequent <code>ngDoCheck()</code>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngAfterViewInit()</code>
      </th>
      <th style="text-align:left">
        <p>Respond after Angular initializes the component&apos;s views and child
          views / the view that a directive is in.</p>
        <p>Called <em>once</em> after the first <a href="https://angular.io/api/core/AfterContentChecked#ngAfterContentChecked"><code>ngAfterContentChecked()</code></a>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><a href="https://angular.io/api/core/AfterViewChecked#ngAfterViewChecked"><code>ngAfterViewChecked()</code></a>
      </th>
      <th style="text-align:left">
        <p>Respond after Angular checks the component&apos;s views and child views
          / the view that a directive is in.</p>
        <p>Called after the <code>ngAfterViewInit</code> and every subsequent <a href="https://angular.io/api/core/AfterContentChecked#ngAfterContentChecked"><code>ngAfterContentChecked()</code></a>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table><table>
  <thead>
    <tr>
      <th style="text-align:left"><code>ngOnDestroy()</code>
      </th>
      <th style="text-align:left">
        <p>Cleanup just before Angular destroys the directive/component. Unsubscribe
          Observables and detach event handlers to avoid memory leaks.</p>
        <p>Called <em>just before</em> Angular destroys the directive/component.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>Use `ngOnInit()` for two main reasons:

1. To perform complex initializations shortly after construction. \_\_ An `ngOnInit()` is a good place for a component to fetch its initial data. 
2. To set up the component after Angular sets the input properties.

Don't fetch data in a component constructor. Constructors should do no more than set the initial local variables to simple values.

Remember also that a directive's data-bound input properties are not set until _after construction_. That's a problem if you need to initialize the directive based on those properties. They'll have been set when `ngOnInit()` runs.

{% hint style="info" %}
The `ngOnChanges()` method is your first opportunity to access those properties. Angular calls `ngOnChanges()` before `ngOnInit()` and many times after that. It only calls `ngOnInit()` once.
{% endhint %}

## _OnDestroy\(\)_

Put cleanup logic in `ngOnDestroy()`, the logic that _must_ run before Angular destroys the directive. \_\_This is the place to free resources that won't be garbage collected automatically.

1. Unsubscribe from Observables and DOM events.
2. Stop interval timers.
3. Unregister all callbacks that this directive registered with global or application services.

   You risk memory leaks if you neglect to do so.

## _OnChanges\(\)_

Angular calls its `ngOnChanges()` method whenever it detects changes to _**input properties**_ of the component \(or directive\).

```typescript
ngOnChanges(changes: SimpleChanges) {
  for (let propName in changes) {
    let chng = changes[propName];
    let cur  = JSON.stringify(chng.currentValue);
    let prev = JSON.stringify(chng.previousValue);
    this.changeLog.push(`${propName}: currentValue = ${cur}, previousValue = ${prev}`);
  }
}
```

## _DoCheck\(\)_

Use the [`DoCheck`](https://angular.io/api/core/DoCheck) hook to detect and act upon changes that Angular doesn't catch on its own. \_\_This method will be called when user click the input but didn't change the value.

