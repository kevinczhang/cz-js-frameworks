---
description: >-
  Observables provide support for passing messages between publishers and
  subscribers in your application.
---

# Observables & RxJS

 Observables are declarative—that is, you define a function for publishing values, but it is not executed until a consumer subscribes to it. The subscribed consumer then receives notifications until the function completes, or until they unsubscribe.

 An observable can deliver multiple values of any type—literals, messages, or events, depending on the context.  Whether the stream was keystrokes, an HTTP response, or an interval timer, the interface for listening to values and stopping listening is the same.

## Defining observers

 A handler for receiving observable notifications implements the `Observer` interface. It is an object that defines callback methods to handle the three types of notifications that an observable can send:

| NOTIFICATION TYPE | DESCRIPTION |
| :--- | :--- |
| `next` | Required. A handler for each delivered value. Called zero or more times after execution starts. |
| `error` | Optional. A handler for an error notification. An error halts execution of the observable instance. |
| `complete` | Optional. A handler for the execution-complete notification. Delayed values can continue to be delivered to the next handler after execution is complete. |

## Subscribing

 An `Observable` instance begins publishing values only when someone subscribes to it. You subscribe by calling the `subscribe()` method of the instance, passing an observer object to receive the notifications.

```typescript
// Create simple observable that emits three values
const myObservable = of(1, 2, 3);

// Create observer object
const myObserver = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

// Execute with the observer object
myObservable.subscribe(myObserver);
// Logs:
// Observer got a next value: 1
// Observer got a next value: 2
// Observer got a next value: 3
// Observer got a complete notification
```

