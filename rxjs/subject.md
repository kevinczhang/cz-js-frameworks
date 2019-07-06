# Subject

An RxJS Subject is a special type of Observable that allows values to be multicasted to many Observers. While plain Observables are unicast \(each subscribed Observer owns an independent execution of the Observable\), Subjects are multicast.

> A Subject is like an Observable, but can multicast to many Observers. Subjects are like EventEmitters: they maintain a registry of many listeners.

## BehaviorSubject

BehaviorSubjects are useful for representing "values over time". For instance, an event stream of birthdays is a Subject, but the stream of a person's age would be a BehaviorSubject.

```typescript
import { BehaviorSubject } from 'rxjs';
const subject = new BehaviorSubject(0); // 0 is the initial value

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(3);

// Logs
// observerA: 0
// observerA: 1
// observerA: 2
// observerB: 2
// observerA: 3
// observerB: 3
```

## ReplaySubject

A ReplaySubject is similar to a BehaviorSubject in that it can send old values to new subscribers, but it can also record a part of the Observable execution.

A ReplaySubject records multiple values from the Observable execution and replays them to new subscribers.

