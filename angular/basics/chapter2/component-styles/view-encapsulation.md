---
description: >-
  In Angular, a component's styles can be encapsulated within the component's
  host element so that they don't affect the rest of the application.
---

# View encapsulation

| MODES                                                                                    | DETAILS                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`ViewEncapsulation.ShadowDom`](https://angular.io/api/core/ViewEncapsulation#ShadowDom) | Angular uses the browser's built-in [Shadow DOM API](https://developer.mozilla.org/docs/Web/Web\_Components/Shadow\_DOM) to enclose the component's view inside a ShadowRoot, used as the component's host element, and apply the provided styles in an isolated manner.                                        |
| [`ViewEncapsulation.Emulated`](https://angular.io/api/core/ViewEncapsulation#Emulated)   | Angular modifies the component's CSS selectors so that they are only applied to the component's view and do not affect other elements in the application, _emulating_ Shadow DOM behavior. For more details, see [Inspecting generated CSS](https://angular.io/guide/view-encapsulation#inspect-generated-css). |
| [`ViewEncapsulation.None`](https://angular.io/api/core/ViewEncapsulation#None)           | Angular does not apply any sort of view encapsulation meaning that any styles specified for the component are actually globally applied and can affect any HTML element present within the application. This mode is essentially the same as including the styles into the HTML itself.                         |

```typescript
@Component({
  selector: 'app-no-encapsulation',
  template: `
    <h2>None</h2>
    <div class="none-message">No encapsulation</div>
  `,
  styles: ['h2, .none-message { color: red; }'],
  encapsulation: ViewEncapsulation.None,
})
export class NoEncapsulationComponent { }
```
