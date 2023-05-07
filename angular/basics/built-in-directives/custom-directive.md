# Custom directive

We can use attribute selector or css selector such as a class name

```typescript
@Directive({
  selector: "[ccCardHover]"
})
class CardHoverDirective {
  constructor(private el: ElementRef,
              private renderer: Renderer) {
    //noinspection TypeScriptUnresolvedVariable,TypeScriptUnresolvedFunction
    renderer.setElementStyle(el.nativeElement, 'backgroundColor', 'gray');
  }
}
```

&#x20;When the directive gets created Angular can inject an instance of something called `ElementRef` into its constructor.  The `ElementRef` gives the directive _direct access_ to the DOM element upon which it’s attached.

## HostListener & HostBinding



## Inputs & Configuration
