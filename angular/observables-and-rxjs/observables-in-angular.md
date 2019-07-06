---
description: >-
  Angular makes use of observables as an interface to handle a variety of common
  asynchronous operations.
---

# Observables in Angular

## Event emitter

 Angular provides an [`EventEmitter`](https://angular.io/api/core/EventEmitter) class that is used when publishing values from a component through the `@`[`Output`](https://angular.io/api/core/Output)`()` decorator. [`EventEmitter`](https://angular.io/api/core/EventEmitter) extends `Observable`, adding an [`emit()`](https://angular.io/api/core/EventEmitter#emit) method so it can send arbitrary values. When you call [`emit()`](https://angular.io/api/core/EventEmitter#emit), it passes the emitted value to the `next()` method of any subscribed observer.

## HTTP

 Angular’s [`HttpClient`](https://angular.io/api/common/http/HttpClient) returns observables from HTTP method calls. 

* Observables do not mutate the server response \(as can occur through chained `.then()` calls on promises\). Instead, you can use a series of operators to transform values as needed.
* HTTP requests are cancellable through the [`unsubscribe()`](https://angular.io/api/service-worker/SwPush#unsubscribe) method.
* Requests can be configured to get progress event updates.
* Failed requests can be retried easily.

## Async pipe

 The [AsyncPipe](https://angular.io/api/common/AsyncPipe) subscribes to an observable or promise and returns the latest value it has emitted. When a new value is emitted, the pipe marks the component to be checked for changes.

```typescript
@Component({
  selector: 'async-observable-pipe',
  template: `<div><code>observable|async</code>:
       Time: {{ time | async }}</div>`
})
export class AsyncObservablePipeComponent {
  time = new Observable(observer =>
    setInterval(() => observer.next(new Date().toString()), 1000)
  );
}
```

## Router

 [`Router.events`](https://angular.io/api/router/Router#events) provides events as observables. You can use the [`filter()`](https://angular.io/api/core/QueryList#filter) operator from RxJS to look for events of interest, and subscribe to them in order to make decisions based on the sequence of events in the navigation process. 

{% code-tabs %}
{% code-tabs-item title="Router events" %}
```typescript
import { Router, NavigationStart } from '@angular/router';
import { filter } from 'rxjs/operators';

@Component({
  selector: 'app-routable',
  templateUrl: './routable.component.html',
  styleUrls: ['./routable.component.css']
})
export class Routable1Component implements OnInit {

  navStart: Observable<NavigationStart>;

  constructor(private router: Router) {
    // Create a new Observable the publishes only the NavigationStart event
    this.navStart = router.events.pipe(
      filter(evt => evt instanceof NavigationStart)
    ) as Observable<NavigationStart>;
  }

  ngOnInit() {
    this.navStart.subscribe(evt => console.log('Navigation Started!'));
  }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="ActivatedRoute" %}
```typescript
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-routable',
  templateUrl: './routable.component.html',
  styleUrls: ['./routable.component.css']
})
export class Routable2Component implements OnInit {
  constructor(private activatedRoute: ActivatedRoute) {}

  ngOnInit() {
    this.activatedRoute.url
      .subscribe(url => console.log('The URL changed to: ' + url));
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}



