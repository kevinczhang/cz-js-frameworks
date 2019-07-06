---
description: A pipe takes in data as input and transforms it to a desired output.
---

# Pipes

## Parameterizing a pipe

A pipe can accept any number of optional parameters to fine-tune its output. To add parameters to a pipe, follow the pipe name with a colon \( : \) and then the parameter value \(such as `currency:'EUR'`\). If the pipe accepts multiple parameters, separate the values with colons \(such as `slice:1:5`\).

```typescript
@Component({
  selector: 'hero-birthday2',
  template: `
    <p>The hero's birthday is {{ birthday | date:format }}</p>
    <button (click)="toggleFormat()">Toggle Format</button>
  `
})
export class HeroBirthday2Component {
  birthday = new Date(1988, 3, 15); // April 15, 1988
  toggle = true; // start with true == shortDate

  get format()   { return this.toggle ? 'shortDate' : 'fullDate'; }
  toggleFormat() { this.toggle = !this.toggle; }
}
```

## Chaining pipes

You can chain pipes together in potentially useful combinations.

```typescript
The chained hero's birthday is
{{  birthday | date:'fullDate' | uppercase}}
```

## Custom pipes

{% code-tabs %}
{% code-tabs-item title="exponential-strength.pipe.ts" %}
```typescript
import { Pipe, PipeTransform } from '@angular/core';
/*
 * Raise the value exponentially
 * Takes an exponent argument that defaults to 1.
 * Usage:
 *   value | exponentialStrength:exponent
 * Example:
 *   {{ 2 | exponentialStrength:10 }}
 *   formats to: 1024
*/
@Pipe({name: 'exponentialStrength'})
export class ExponentialStrengthPipe implements PipeTransform {
  transform(value: number, exponent: string): number {
    let exp = parseFloat(exponent);
    return Math.pow(value, isNaN(exp) ? 1 : exp);
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="power-boost-calculator.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-power-boost-calculator',
  template: `
    <h2>Power Boost Calculator</h2>
    <div>Normal power: <input [(ngModel)]="power"></div>
    <div>Boost factor: <input [(ngModel)]="factor"></div>
    <p>
      Super Hero Power: {{power | exponentialStrength: factor}}
    </p>
  `
})
export class PowerBoostCalculatorComponent {
  power = 5;
  factor = 1;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Pure and impure pipes

There are two categories of pipes: _pure_ and _impure_. Pipes are pure by default. Every pipe you've seen so far has been pure. You make a pipe impure by setting its pure flag to false. You could make the `FlyingHeroesPipe` impure like this:

```typescript
@Pipe({
  name: 'flyingHeroesImpure',
  pure: false
})
```

### Pure pipes

Angular executes a _pure pipe_ only when it detects a _pure change_ to the input value. A pure change is either a change to a primitive input value \(`String`, `Number`, `Boolean`, `Symbol`\) or a changed object reference \(`Date`, `Array`, `Function`, `Object`\).

### Impure pipes

Angular executes an _impure pipe_ during every component change detection cycle. An impure pipe is called often, as often as every keystroke or mouse-move.

With that concern in mind, implement an impure pipe with great care. An expensive, long-running pipe could destroy the user experience.

## The impure AsyncPipe

The Angular [`AsyncPipe`](https://angular.io/api/common/AsyncPipe) is an interesting example of an impure pipe. The [`AsyncPipe`](https://angular.io/api/common/AsyncPipe) accepts a `Promise` or `Observable` as input and subscribes to the input automatically, eventually returning the emitted values.

The [`AsyncPipe`](https://angular.io/api/common/AsyncPipe) is also stateful. The pipe maintains a subscription to the input `Observable` and keeps delivering values from that `Observable` as they arrive.

