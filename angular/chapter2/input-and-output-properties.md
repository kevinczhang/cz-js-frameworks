---
description: >-
  You can only bind to another component or directive through its Input and
  Output properties.
---

# Input and Output properties

An _Input_ property is a _settable_ property annotated with an `@`[`Input`](https://angular.io/api/core/Input) decorator. Values flow _into_ the property when it is data bound with a [property binding](https://angular.io/guide/template-syntax#property-binding)

An _Output_ property is an _observable_ property annotated with an `@`[`Output`](https://angular.io/api/core/Output) decorator. The property almost always returns an Angular [`EventEmitter`](https://angular.io/api/core/EventEmitter). Values flow _out_ of the component as events bound with an [event binding](https://angular.io/guide/template-syntax#event-binding).

{% hint style="warning" %}
All data bound properties must be TypeScript _public_ properties. Angular never binds to a TypeScript _private_ property.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="voter.component.ts" %}
```typescript
import { Component, EventEmitter, Input, Output } from '@angular/core';

@Component({
  selector: 'app-voter',
  template: `
    <h4>{{name}}</h4>
    <button (click)="vote(true)"  [disabled]="didVote">Agree</button>
    <button (click)="vote(false)" [disabled]="didVote">Disagree</button>
  `
})
export class VoterComponent {
  @Input()  name: string;
  @Output() voted = new EventEmitter<boolean>();
  didVote = false;

  vote(agreed: boolean) {
    this.voted.emit(agreed);
    this.didVote = true;
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="votetaker.component.ts" %}
```text
import { Component }      from '@angular/core';

@Component({
  selector: 'app-vote-taker',
  template: `
    <h2>Should mankind colonize the Universe?</h2>
    <h3>Agree: {{agreed}}, Disagree: {{disagreed}}</h3>
    <app-voter *ngFor="let voter of voters"
      [name]="voter"
      (voted)="onVoted($event)">
    </app-voter>
  `
})
export class VoteTakerComponent {
  agreed = 0;
  disagreed = 0;
  voters = ['Mr. IQ', 'Ms. Universe', 'Bombasto'];

  onVoted(agreed: boolean) {
    agreed ? this.agreed++ : this.disagreed++;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Intercept input property changes with a setter  <a id="intercept-input-property-changes-with-a-setter"></a>

Use an input property setter to intercept and act upon a value from the parent.

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-name-child',
  template: '<h3>"{{name}}"</h3>'
})
export class NameChildComponent {
  private _name = '';

  @Input()
  set name(name: string) {
    this._name = (name && name.trim()) || '<no name set>';
  }

  get name(): string { return this._name; }
}
```

## Input or output?

_Input_ properties usually receive data values. _Output_ properties expose event producers, such as [`EventEmitter`](https://angular.io/api/core/EventEmitter) objects.

![](../../.gitbook/assets/image%20%287%29.png)

## Aliasing input/output properties

You can specify the alias for the property name by passing it into the input/output decorator like this:

```typescript
@Output('myClick') clicks = new EventEmitter<string>(); //  @Output(alias) propertyName = ...
```

