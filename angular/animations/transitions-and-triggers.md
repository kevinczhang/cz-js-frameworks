# Transitions and triggers

 Angular's animation support builds on top of web animations, so you can animate any property that the browser considers animatable. This includes positions, sizes, transforms, colors, borders, and more. The W3C maintains a list of animatable properties on its [CSS Transitions](https://www.w3.org/TR/css-transitions-1/) page.

## Predefined states and wildcard matching

#### Wildcard state <a id="wildcard-state"></a>

 An asterisk `*` or _wildcard_ matches any animation state. This is useful for defining transitions that apply regardless of the HTML element's start or end state.

 The `* => *` transition applies when any change between two states takes place.

#### Void state <a id="void-state"></a>

 You can use the `void` state to configure transitions for an element that is entering or leaving a page. You can combine wildcard and void states in a transition to trigger animations that enter and leave the page:

* A transition of `* => void` applies when the element leaves a view, regardless of what state it was in before it left.
* A transition of `void => *` applies when the element enters a view, regardless of what state it assumes when entering.
* The wildcard state `*` matches to _any_ state, including `void`.

### :enter and :leave aliases <a id="enter-and-leave-aliases"></a>

 `:enter` and `:leave` are aliases for the `void => *` and `* => void` transitions. These aliases are used by several animation functions.

```typescript
transition ( ':enter', [ ... ] );  // alias for void => *
transition ( ':leave', [ ... ] );  // alias for * => void
```

 The `:enter` transition runs when any `*`[`ngIf`](https://angular.io/api/common/NgIf) or `*`[`ngFor`](https://angular.io/api/common/NgForOf) views are placed on the page, and `:leave` runs when those views are removed from the page.

### :increment and :decrement in transitions <a id="increment-and-decrement-in-transitions"></a>

 The [`transition`](https://angular.io/api/animations/transition)`()` function takes additional selector values, `:increment` and `:decrement`. Use these to kick off a transition when a numeric value has increased or decreased in value.

## Multiple animation triggers

#### Parent-child animations <a id="parent-child-animations"></a>

 Each time an animation is triggered in Angular, the parent animation always get priority and child animations are blocked. In order for a child animation to run, the parent animation must query each of the elements containing child animations and then allow the animations to run using the [`animateChild()`](https://angular.io/api/animations/animateChild) function.

**Disabling an animation on an HTML element**

 A special animation control binding called `@.disabled` can be placed on an HTML element to disable animations on that element, as well as any nested elements. When true, the `@.disabled` binding prevents all animations from rendering.

 To disable all animations for an Angular app, place the `@.disabled` host binding on the topmost Angular component.

```typescript
@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.css'],
  animations: [
    slideInAnimation
    // animation triggers go here
  ]
})
export class AppComponent {
  @HostBinding('@.disabled')
  public animationsDisabled = false;
}
```

## Animation callbacks

 The animation [`trigger`](https://angular.io/api/animations/trigger)`()` function emits _callbacks_ when it starts and when it finishes.  In the HTML template, the animation event is passed back via `$event`, as `@trigger.start` and `@trigger.done`, where [`trigger`](https://angular.io/api/animations/trigger) is the name of the trigger being used. In our example, the trigger `openClose` appears as follows.

```markup
<div [@openClose]="isOpen ? 'open' : 'closed'"
    (@openClose.start)="onAnimationEvent($event)"
    (@openClose.done)="onAnimationEvent($event)"
    class="open-close-container">
</div>
```

 Callbacks can serve as a debugging tool, for example in conjunction with `console.warn()` to view the application's progress in a browser's Developer JavaScript Console. The following code snippet creates console log output for our original example, a button with the two states of `open` and `closed`.

```typescript
export class OpenCloseComponent {
  onAnimationEvent ( event: AnimationEvent ) {
    // openClose is trigger name in this example
    console.warn(`Animation Trigger: ${event.triggerName}`);

    // phaseName is start or done
    console.warn(`Phase: ${event.phaseName}`);

    // in our example, totalTime is 1000 or 1 second
    console.warn(`Total time: ${event.totalTime}`);

    // in our example, fromState is either open or closed
    console.warn(`From: ${event.fromState}`);

    // in our example, toState either open or closed
    console.warn(`To: ${event.toState}`);

    // the HTML element itself, the button in this case
    console.warn(`Element: ${event.element}`);
  }
}
```

## Keyframes

 Angular's `keyframe()` function is similar to keyframes in CSS. Keyframes allow several style changes within a single timing segment. 

#### Offset <a id="offset"></a>

 Keyframes include an _offset_ that defines the point in the animation where each style change occurs. Offsets are relative measures from zero to one, marking the beginning and end of the animation, respectively. ****Defining offsets for keyframes is optional. If you omit them, evenly spaced offsets are automatically assigned.

```typescript
transition('* => active', [
  animate('2s', keyframes([
    style({ backgroundColor: 'blue', offset: 0}),
    style({ backgroundColor: 'red', offset: 0.8}),
    style({ backgroundColor: 'orange', offset: 1.0})
  ])),
]),
transition('* => inactive', [
  animate('2s', keyframes([
    style({ backgroundColor: 'orange', offset: 0}),
    style({ backgroundColor: 'red', offset: 0.2}),
    style({ backgroundColor: 'blue', offset: 1.0})
  ]))
]),
```



