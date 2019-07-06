---
description: These operators allow the creation of an observable from nearly anything.
---

# Creation Operators

## from

Creates an Observable from an Array, an array-like object, a Promise, an iterable object, or an Observable-like object.

**from&lt;T&gt;\(input: ObservableInput&lt;T&gt;, scheduler?: SchedulerLike\): Observable&lt;T&gt;**

```text
import { from } from 'rxjs';

const array = [10, 20, 30];
const result = from(array);

result.subscribe(x => console.log(x));
```

## of

Converts the arguments to an observable sequence.

**of&lt;T&gt;\(...args: Array&lt;T \| SchedulerLike&gt;\): Observable&lt;T&gt;**

```text
import { of } from 'rxjs';

of(10, 20, 30)
.subscribe(
  next => console.log('next:', next),
  err => console.log('error:', err),
  () => console.log('the end'),
);
```

