# Component styles

For every Angular component you write, you can define not only an HTML template, but also the CSS styles that go with that template, specifying any selectors, rules, and media queries that you need.&#x20;

You can add global styles to styles.scss file, and also import other style files.

## Special selectors for component styling

### :host

Use the :host pseudo-class selector to target styles in the element that _hosts_ the component (as opposed to targeting elements _inside_ the component's template).

```css
:host(.active) {
  border-width: 3px;
}
```

### :host-context

Sometimes it's useful to apply styles based on some condition _outside_ of a component's view. The `:host-context()` selector looks for a CSS class in any ancestor of the component host element, up to the document root. The `:host-context()` selector is useful when combined with another selector.

The following example applies a `background-color` style to all `<h2>` elements _inside_ the component, only if some ancestor element has the CSS class `theme-light`.

```css
:host-context(.theme-light) h2 {
  background-color: #eef;
}
```
