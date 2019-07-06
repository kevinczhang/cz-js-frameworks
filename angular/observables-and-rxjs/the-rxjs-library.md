---
description: >-
  RxJS (Reactive Extensions for JavaScript) is a library for reactive
  programming using observables that makes it easier to compose asynchronous or
  callback-based code
---

# The RxJS library

## Observable creation functions

###  Create observable examples

{% code-tabs %}
{% code-tabs-item title="From Stream" %}
```typescript
import { fromPromise } from 'rxjs';

// Create an Observable out of a promise
const data = fromPromise(fetch('/api/endpoint'));
// Subscribe to begin listening for async result
data.subscribe({
 next(response) { console.log(response); },
 error(err) { console.error('Error: ' + err); },
 complete() { console.log('Completed'); }
});
```
{% endcode-tabs-item %}

{% code-tabs-item title=" from a counter" %}
```typescript
import { interval } from 'rxjs';

// Create an Observable that will publish a value on an interval
const secondsCounter = interval(1000);
// Subscribe to begin publishing values
secondsCounter.subscribe(n =>
  console.log(`It's been ${n} seconds since subscribing!`));
```
{% endcode-tabs-item %}

{% code-tabs-item title="from an event" %}
```typescript
import { fromEvent } from 'rxjs';

const el = document.getElementById('my-element');

// Create an Observable that will publish mouse movements
const mouseMoves = fromEvent(el, 'mousemove');

// Subscribe to start listening for mouse-move events
const subscription = mouseMoves.subscribe((evt: MouseEvent) => {
  // Log coords of mouse movements
  console.log(`Coords: ${evt.clientX} X ${evt.clientY}`);

  // When the mouse is over the upper-left of the screen,
  // unsubscribe to stop listening for mouse movements
  if (evt.clientX < 40 && evt.clientY < 40) {
    subscription.unsubscribe();
  }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Operators

 Operators are functions that build on the observables foundation to enable sophisticated manipulation of collections. For example, RxJS defines operators such as [`map()`](https://angular.io/api/core/QueryList#map), [`filter()`](https://angular.io/api/core/QueryList#filter), `concat()`, and `flatMap()`.

 You can use _pipes_ to link operators together. Pipes let you combine multiple functions into a single function. The `pipe()` function takes as its arguments the functions you want to combine, and returns a new function that, when executed, runs the composed functions in sequence.

```typescript
import { filter, map } from 'rxjs/operators';

const squareOdd = of(1, 2, 3, 4, 5)
  .pipe(
    filter(n => n % 2 !== 0),
    map(n => n * n)
  );

// Subscribe to get values
squareOdd.subscribe(x => console.log(x));
```

#### Common operators <a id="common-operators"></a>

| AREA | OPERATORS |
| :--- | :--- |
| Creation | `from`, `fromPromise`,`fromEvent`, `of` |
| Combination | `combineLatest`, `concat`, `merge`, `startWith` , `withLatestFrom`, `zip` |
| Filtering | `debounceTime`, `distinctUntilChanged`, `filter`, `take`, `takeUntil` |
| Transformation | `bufferTime`, `concatMap`, `map`, `mergeMap`, `scan`, `switchMap` |
| Utility | `tap` |
| Multicasting | `share` |

## Error handling

 In addition to the [`error()`](https://angular.io/api/common/http/testing/TestRequest#error) handler that you provide on subscription, RxJS provides the `catchError`operator that lets you handle known errors in the observable recipe.

{% code-tabs %}
{% code-tabs-item title="without retry" %}
```typescript
import { ajax } from 'rxjs/ajax';
import { map, catchError } from 'rxjs/operators';
// Return "response" from the API. If an error happens,
// return an empty array.
const apiData = ajax('/api/data').pipe(
  map(res => {
    if (!res.response) {
      throw new Error('Value expected!');
    }
    return res.response;
  }),
  catchError(err => of([]))
);

apiData.subscribe({
  next(x) { console.log('data: ', x); },
  error(err) { console.log('errors already caught... will not run'); }
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="with retry 3" %}
```typescript
import { ajax } from 'rxjs/ajax';
import { map, retry, catchError } from 'rxjs/operators';

const apiData = ajax('/api/data').pipe(
  retry(3), // Retry up to 3 times before failing
  map(res => {
    if (!res.response) {
      throw new Error('Value expected!');
    }
    return res.response;
  }),
  catchError(err => of([]))
);

apiData.subscribe({
  next(x) { console.log('data: ', x); },
  error(err) { console.log('errors already caught... will not run'); }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Naming conventions for observables

 Although the Angular framework does not enforce a naming convention for observables, you will often see observables named with a trailing “$” sign.

```typescript
import { Component } from '@angular/core';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-stopwatch',
  templateUrl: './stopwatch.component.html'
})
export class StopwatchComponent {

  stopwatchValue: number;
  stopwatchValue$: Observable<number>;

  start() {
    this.stopwatchValue$.subscribe(num =>
      this.stopwatchValue = num
    );
  }
}
```

