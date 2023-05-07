---
description: >-
  User actions such as clicking a link, pushing a button, and entering text
  raise DOM events. This page explains how to bind those events to component
  event handlers using the Angular event binding synt
---

# User Input

## Get user input from the $event object

DOM events carry a payload of information that may be useful to the component.

{% tabs %}
{% tab title="keyup.components.ts" %}
```markup
template: `
  <input (keyup)="onKey($event)">
  <p>{{values}}</p>
`
```
{% endtab %}

{% tab title="keyup.components.ts" %}
```typescript
export class KeyUpComponent_v1 {
  values = '';

  onKey(event: any) { // without type info
    this.values += event.target.value + ' | ';
  }
}
```
{% endtab %}

{% tab title="Typed_event" %}
```typescript
export class KeyUpComponent_v1 {
  values = '';


  onKey(event: KeyboardEvent) { // with type info
    this.values += (<HTMLInputElement>event.target).value + ' | ';
  }
}
```
{% endtab %}
{% endtabs %}

### Get user input from a template reference variable   <a href="#get-user-input-from-a-template-reference-variable" id="get-user-input-from-a-template-reference-variable"></a>

```typescript
@Component({
  selector: 'app-key-up4',
  template: `
    <input #box
      (keyup)="onKey(box.value)"
      (keyup.enter)="update(box.value)"
      (blur)="update(box.value)">

    <p>{{value}}</p>
  `
})
export class KeyUpComponent_v4 {
  value = '';
  // listen on all keystroke
  onKey(value: string) {
    this.values += value + ' | ';
  }
  update(value: string) { this.value = value; }
}
```
