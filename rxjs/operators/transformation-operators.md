# Transformation Operators

## ❓ switchMap

The main difference between switchMap and other flattening operators is the **cancelling effect**. On each emission the previous inner observable \(the result of the function you supplied\) is cancelled and the new observable is subscribed. You can remember this by the phrase **switch to a new observable**.

This works perfectly for scenarios like typeaheads where you are no longer concerned with the response of the previous request when a new input arrives.

```typescript
import { interval, fromEvent } from 'rxjs';
import { switchMap } from 'rxjs/operators';

fromEvent(document, 'click')
.pipe(
	// restart counter on every click
	switchMap(() => interval(1000))
)
.subscribe(console.log);
```

## ❓ map

Apply projection with each value from source.

```typescript
import { from } from 'rxjs';
import { map } from 'rxjs/operators';

//emit (1,2,3,4,5)
const source = from([1, 2, 3, 4, 5]);
//add 10 to each value
const example = source.pipe(map(val => val + 10));
//output: 11,12,13,14,15
const subscribe = example.subscribe(val => console.log(val));
```

