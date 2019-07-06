# Animations

#### Step 1: Enabling the animations module <a id="step-1-enabling-the-animations-module"></a>

 Import [`BrowserAnimationsModule`](https://angular.io/api/platform-browser/animations/BrowserAnimationsModule), which introduces the animation capabilities into your Angular root application module.

#### Step 2: Importing animation functions into component files <a id="step-2-importing-animation-functions-into-component-files"></a>

 If you plan to use specific animation functions in component files, import those functions from `@angular/animations`. \( [trigger](https://angular.io/api/animations/trigger), [state](https://angular.io/api/animations/state), [style](https://angular.io/api/animations/style), [animate](https://angular.io/api/animations/animate), [transition](https://angular.io/api/animations/transition)\)

#### Step 3: Adding the animation metadata property <a id="step-3-adding-the-animation-metadata-property"></a>

 In the component file, add a metadata property called `animations:` within the `@`[`Component`](https://angular.io/api/core/Component)`()` decorator. You put the trigger that defines an animation within the `animations` metadata property.

{% code-tabs %}
{% code-tabs-item title="animations.ts" %}
```typescript
@Component({
  selector: 'app-open-close',
  animations: [
    trigger('openClose', [
      // ...
      state('open', style({

        height: '200px',
        opacity: 1,
        backgroundColor: 'yellow'
      })),
      state('closed', style({
        height: '100px',
        opacity: 0.5,
        backgroundColor: 'green'
      })),
      transition('open => closed', [
        animate('1s')
      ]),
      transition('closed => open', [
        animate('0.5s')
      ]),
    ]),
  ],
  templateUrl: 'open-close.component.html',
  styleUrls: ['open-close.component.css']
})
export class OpenCloseComponent {
  isOpen = true;

  toggle() {
    this.isOpen = !this.isOpen;
  }

}
```
{% endcode-tabs-item %}

{% code-tabs-item title="animations.html" %}
```markup
<div [@triggerName]="expression">...</div>;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Animations API summary <a id="animations-api-summary"></a>

| Function name | What it does |
| :--- | :--- |
| [`trigger`](https://angular.io/api/animations/trigger)`()` | Kicks off the animation and serves as a container for all other animation function calls. HTML template binds to [`triggerName`](https://angular.io/api/animations/AnimationEvent#triggerName). Use the first argument to declare a unique trigger name. Uses array syntax. |
| [`style`](https://angular.io/api/animations/style)`()` | Defines one or more CSS styles to use in animations. Controls the visual appearance of HTML elements during animations. Uses object syntax. |
| [`state`](https://angular.io/api/animations/state)`()` | Creates a named set of CSS styles that should be applied on successful transition to a given state. The state can then be referenced by name within other animation functions. |
| [`animate()`](https://angular.io/api/animations/browser/testing/MockAnimationDriver#animate) | Specifies the timing information for a transition. Optional values for `delay` and [`easing`](https://angular.io/api/animations/browser/testing/MockAnimationPlayer#easing). Can contain [`style`](https://angular.io/api/animations/style)`()` calls within. |
| [`transition`](https://angular.io/api/animations/transition)`()` | Defines the animation sequence between two named states. Uses array syntax. |
| [`keyframes`](https://angular.io/api/animations/keyframes)`()` | Allows a sequential change between styles within a specified time interval. Use within [`animate()`](https://angular.io/api/animations/browser/testing/MockAnimationDriver#animate). Can include multiple [`style`](https://angular.io/api/animations/style)`()` calls within each `keyframe()`. Uses array syntax. |
| [`group()`](https://angular.io/api/forms/FormBuilder#group) | Specifies a group of animation steps \(_inner animations_\) to be run in parallel. Animation continues only after all inner animation steps have completed. Used within [`sequence`](https://angular.io/api/animations/sequence)`()`or [`transition`](https://angular.io/api/animations/transition)`().` |
| [`query()`](https://angular.io/api/animations/browser/testing/MockAnimationDriver#query) | Use to find one or more inner HTML elements within the current element. |
| [`sequence`](https://angular.io/api/animations/sequence)`()` | Specifies a list of animation steps that are run sequentially, one by one. |
| [`stagger`](https://angular.io/api/animations/stagger)`()` | Staggers the starting time for animations for multiple elements. |
| [`animation`](https://angular.io/api/animations/animation)`()` | Produces a reusable animation that can be invoked from elsewhere. Used together with [`useAnimation`](https://angular.io/api/animations/useAnimation)`()`. |
| [`useAnimation`](https://angular.io/api/animations/useAnimation)`()` | Activates a reusable animation. Used with [`animation`](https://angular.io/api/animations/animation)`()`. |
| [`animateChild`](https://angular.io/api/animations/animateChild)`()` | Allows animations on child components to be run within the same timeframe as the parent. |

