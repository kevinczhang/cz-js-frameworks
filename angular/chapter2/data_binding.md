# Data binding

In fact, once you start data binding, you are no longer working with HTML attributes. You aren't setting attributes. You are setting the properties of DOM elements, components, and directives.

## HTML attribute vs. DOM property

The distinction between an HTML attribute and a DOM property is crucial to understanding how Angular binding works.

**Attributes are defined by HTML. Properties are defined by the DOM \(Document Object Model\).**

A few HTML attributes have 1:1 mapping to properties. id is one example.

Some HTML attributes don't have corresponding properties. colspan is one example.

Some DOM properties don't have corresponding attributes. textContent is one example.

Many HTML attributes appear to map to properties ... but not in the way you might think!

That last category is confusing until you grasp this general rule:

**Attributes initialize DOM properties and then they are done. Property values can change; attribute values can't.**

## Binding targets _\*\*_

The target of a data binding is something in the DOM.

{% tabs %}
{% tab title="Property" %}
Element property  
Component property  
Directive property

You should omit the brackets when all of the following are true:

* The target property accepts a string value.
* The string is a fixed value that you can bake into the template.
* This initial value never changes.

```markup
<img [src]="heroImageUrl">
<app-hero-detail [hero]="currentHero"></app-hero-detail>
<div [ngClass]="{'special': isSpecial}"></div>

<app-hero-detail prefix="You are my" [hero]="currentHero"></app-hero-detail>
```
{% endtab %}

{% tab title="Event" %}
Element Event  
Component Event  
Directive Event

Directives typically raise custom events with an Angular **EventEmitter**. The directive creates an EventEmitter and exposes it as a property. The directive calls EventEmitter.emit\(payload\) to fire an event, passing in a message payload, which can be anything.

```markup
<button (click)="onSave()">Save</button>
<app-hero-detail (deleteRequest)="deleteHero()"></app-hero-detail>
<div (myClick)="clicked=$event" clickable>click me</div>
```
{% endtab %}

{% tab title="Two-way" %}
Event and property

```markup
<input [(ngModel)]="name">
```
{% endtab %}

{% tab title="Attribute" %}
Attribute \(the exception\) This is the only exception to the rule that a binding sets a target property. This is the only binding that creates and sets an attribute.

**You must use attribute binding when there is no element property to bind.**

```markup
<button [attr.aria-label]="help">help</button>
<tr><td [attr.colspan]="1 + 1">One-Two</td></tr>
```
{% endtab %}

{% tab title="Class" %}
class property You can add and remove CSS class names from an element's class attribute with a class binding.

**While this is a fine way to toggle a single class name, the NgClass directive is usually preferred when managing multiple class names at the same time.**

```markup
<div [class.special]="isSpecial">Special</div>
```
{% endtab %}

{% tab title="Style" %}
style property You can set inline styles with a style binding.

**While this is a fine way to set a single style, the NgStyle directive is generally preferred when setting several inline styles at the same time.**

```markup
<button [style.color]="isSpecial ? 'red' : 'green'">
```
{% endtab %}
{% endtabs %}

