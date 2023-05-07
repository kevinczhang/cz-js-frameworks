# Class and Style Bindings

## Syntax for class

### Object&#x20;

```markup
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
```

Or

```markup
<div v-bind:class="classObject"></div>
```

```javascript
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

### Array Syntax

```javascript
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

### With Components

&#x20;When you use the `class` attribute on a custom component, those classes will be added to the component’s root element. Existing classes on this element will not be overwritten.

## Syntax for style

### Object

```javascript
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

Or

```javascript
<div v-bind:style="styleObject"></div>
```

```javascript
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

```javascript
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

