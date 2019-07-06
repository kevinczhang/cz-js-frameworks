---
description: >-
  These are Observable creation operators that also have join functionality --
  emitting values of multiple source Observables.
---

# Join Creation Operators

## ❓ combineLatest

Combines multiple Observables to create an Observable whose values are calculated from the latest values of each of its input Observables.

**combineLatest&lt;O extends ObservableInput&lt;any&gt;, R&gt;\(...observables: \(O \| \(\(...values: ObservedValueOf&lt;O&gt;\[\]\) =&gt; R\) \| SchedulerLike\)\[\]\): Observable&lt;R&gt;**

#### Returns

`Observable<R>`: An Observable of projected values from the most recent values from each input Observable, or an array of the most recent values from each input Observable.

> Whenever any input Observable emits a value, it computes a formula using the latest values from all the inputs, then emits the output of that formula.

There timed events

```typescript
import { combineLatest, of } from 'rxjs';
import { delay, starWith } from 'rxjs/operators';

const observables = [1, 5, 10].map(
  n => of(n).pipe(
    delay(n * 1000),   // emit 0 and then emit n after n seconds
    startWith(0),
  )
);
const combined = combineLatest(observables);
combined.subscribe(value => console.log(value));
// Logs
// [0, 0, 0] immediately
// [1, 0, 0] after 1s
// [1, 5, 0] after 5s
// [1, 5, 10] after 10s
```

Only the last weight is used

```typescript
import { combineLatest, of } from 'rxjs';
import { map } from 'rxjs/operators';

const weight = of(70, 72, 76, 79, 75);
const height = of(1.76, 1.77, 1.78);
const bmi = combineLatest(weight, height).pipe(
  map(([w, h]) => w / (h * h)),
);
bmi.subscribe(x => console.log('BMI is ' + x));

// With output to console:
// BMI is 24.212293388429753
// BMI is 23.93948099205209
// BMI is 23.671253629592222
```

## ❓ concat

Creates an output Observable which sequentially emits all values from given Observable and then moves on to the next.

**concat&lt;O extends ObservableInput&lt;any&gt;, R&gt;\(...observables: Array&lt;O \| SchedulerLike&gt;\): Observable&lt;ObservedValueOf&lt;O&gt; \| R&gt;**

#### Returns

`Observable<ObservedValueOf<O> | R>`: All values of each passed Observable merged into a single Observable, in order, in serial fashion.

```typescript
import { of, concat } from 'rxjs';
import { delay } from 'rxjs/operators';

concat(
  of(1, 2, 3).pipe(delay(3000)),
  // after 3s, the first observable will complete and 
	// subsquent observable subscribed with values emitted
  of(4, 5, 6)
)
  // log: 1,2,3,4,5,6
  .subscribe(console.log);
```

## ❓ merge

Creates an output Observable which concurrently emits all values from every given input Observable.

**merge&lt;T, R&gt;\(...observables: Array&lt;ObservableInput&lt;any&gt; \| SchedulerLike \| number&gt;\): Observable&lt;R&gt;**

#### Returns

`Observable<R>`: an Observable that emits items that are the result of every input Observable.

```typescript
import { merge, interval } from 'rxjs';
import { take } from 'rxjs/operators';

const timer1 = interval(1000).pipe(take(10));
const timer2 = interval(2000).pipe(take(6));
const timer3 = interval(500).pipe(take(10));
const concurrent = 2; // the argument
const merged = merge(timer1, timer2, timer3, concurrent);
merged.subscribe(x => console.log(x));

// Results in the following:
// - First timer1 and timer2 will run concurrently
// - timer1 will emit a value every 1000ms for 10 iterations
// - timer2 will emit a value every 2000ms for 6 iterations
// - after timer1 hits it's max iteration, timer2 will
//   continue, and timer3 will start to run concurrently with timer2
// - when timer2 hits it's max iteration it terminates, and
//   timer3 will continue to emit a value every 500ms until it is complete
```

## ❓ zip

Combines multiple Observables to create an Observable whose values are calculated from the values, in order, of each of its input Observables.

**zip&lt;O extends ObservableInput&lt;any&gt;, R&gt;\(...observables: Array&lt;O \| \(\(...values: ObservedValueOf&lt;O&gt;\[\]\) =&gt; R\)&gt;\): Observable&lt;ObservedValueOf&lt;O&gt;\[\] \| R&gt;**

### **Description**

If the last parameter is a function, this function is used to compute the created value from the input values. Otherwise, an array of the input values is returned.

```typescript
import { zip, of } from 'rxjs';
import { map } from 'rxjs/operators';

let age$ = of<number>(27, 25, 29);
let name$ = of<string>('Foo', 'Bar', 'Beer');
let isDev$ = of<boolean>(true, true, false);

zip(age$, name$, isDev$).pipe(
  map(([age, name, isDev]) => ({ age, name, isDev })),
)
.subscribe(x => console.log(x));

// outputs
// { age: 27, name: 'Foo', isDev: true }
// { age: 25, name: 'Bar', isDev: true }
// { age: 29, name: 'Beer', isDev: false }
```

