# Template reference variables \( \#var \)

A **template reference variable** is often a reference to a DOM element within a template. It can also be a reference to an Angular component or directive or a [web component](https://developer.mozilla.org/en-US/docs/Web/Web_Components). You can refer to a template reference variable _anywhere_ in the template.

```markup
<form (ngSubmit)="onSubmit(heroForm)" #heroForm="ngForm">
  <div class="form-group">
    <label for="name">Name
      <input class="form-control" name="name" required [(ngModel)]="hero.name">
    </label>
  </div>
  <button type="submit" [disabled]="!heroForm.form.valid">Submit</button>
</form>
<div [hidden]="!heroForm.form.valid">
  {{submitMessage}}
</div>
```

The scope of a reference variable is the _entire template_. Do not define the same variable name more than once in the same template. The runtime value will be unpredictable.

## Parent interacts with child via _local variable_  <a id="parent-interacts-with-child-via-local-variable"></a>

The parent component cannot data bind to the child's methods nor to its property. But You can place a local variable, `#timer`, on the tag of child component representing the child component. That gives you a reference to the child component and the ability to access _any of its properties or methods_ from within the parent template.

## Parent calls an _@ViewChild\(\)_  <a id="parent-calls-an-viewchild"></a>

You can't use the _local variable_ technique if an instance of the parent component _class_ must read or write child component values or must call child component methods. _\_When the parent component \_class_ requires that kind of access, _**inject**_ the child component into the parent as a _ViewChild_.

```typescript
import { AfterViewInit, ViewChild } from '@angular/core';
import { Component }                from '@angular/core';
import { CountdownTimerComponent }  from './countdown-timer.component';

@Component({
  selector: 'app-countdown-parent-vc',
  template: `
  <h3>Countdown to Liftoff (via ViewChild)</h3>
  <button (click)="start()">Start</button>
  <button (click)="stop()">Stop</button>
  <div class="seconds">{{ seconds() }}</div>
  <app-countdown-timer></app-countdown-timer>
  `,
  styleUrls: ['../assets/demo.css']
})
export class CountdownViewChildParentComponent implements AfterViewInit {

  @ViewChild(CountdownTimerComponent)
  private timerComponent: CountdownTimerComponent;

  seconds() { return 0; }

  ngAfterViewInit() {
    // Redefine `seconds()` to get from the `CountdownTimerComponent.seconds` ...
    // but wait a tick first to avoid one-time devMode
    // unidirectional-data-flow-violation error
    setTimeout(() => this.seconds = () => this.timerComponent.seconds, 0);
  }

  start() { this.timerComponent.start(); }
  stop() { this.timerComponent.stop(); }
}
```

