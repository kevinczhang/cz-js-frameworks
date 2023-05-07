# Rendering

## Template Syntax

Vue.js uses an HTML-based template syntax that allows you to declaratively bind the rendered DOM to the underlying Vue instance’s data.

Under the hood, Vue compiles the templates into Virtual DOM render functions. Combined with the reactivity system, Vue is able to intelligently figure out the minimal number of components to re-render and apply the minimal amount of DOM manipulations when the app state changes.

## Interpolations

```javascript
<span>Message: {{ msg }}</span>
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
<div v-bind:id="dynamicId"></div>
<button v-bind:disabled="isButtonDisabled">Button</button>
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

## Directives

&#x20;Directives are special attributes with the `v-` prefix. Directive attribute values are expected to be **a single JavaScript expression** (with the exception of `v-for`, which will be discussed later). A directive’s job is to reactively apply side effects to the DOM when the value of its expression changes.&#x20;

```javascript
<p v-if="seen">Now you see me</p>
```

### Arguments

&#x20;Some directives can take an “argument”, denoted by a colon after the directive name. For example, the `v-bind` directive is used to reactively update an HTML attribute:

```javascript
<a v-bind:href="url"> ... </a>
```

&#x20;Here `href` is the argument, which tells the `v-bind` directive to bind the element’s `href` attribute to the value of the expression `url`.

### Dynamic Arguments

Starting in version 2.6.0, it is also possible to use a JavaScript expression in a directive argument by wrapping it with square brackets:

```javascript
<a v-bind:[attributeName]="url"> ... </a>
```

&#x20;Here `attributeName` will be dynamically evaluated as a JavaScript expression, and its evaluated value will be used as the final value for the argument. For example, if your Vue instance has a data property, `attributeName`, whose value is `"href"`, then this binding will be equivalent to `v-bind:href`.

**Dynamic Argument Value Constraints**

Dynamic arguments are expected to evaluate to a string, with the exception of `null`. The special value `null` can be used to explicitly remove the binding. Any other non-string value will trigger a warning.

**Dynamic Argument Expression Constraints**

Dynamic argument expressions have some syntax constraints because certain characters, such as spaces and quotes, are invalid inside HTML attribute names.&#x20;

### Modifiers

&#x20;Modifiers are special postfixes denoted by a dot, which indicate that a directive should be bound in some special way. For example, the `.prevent` modifier tells the `v-on` directive to call `event.preventDefault()` on the triggered event:

```javascript
<form v-on:submit.prevent="onSubmit"> ... </form>
```

## Shorthands

#### `v-bind` Shorthand <a href="#v-bind-shorthand" id="v-bind-shorthand"></a>

```javascript
<!-- full syntax -->
<a v-bind:href="url"> ... </a>

<!-- shorthand -->
<a :href="url"> ... </a>

<!-- shorthand with dynamic argument (2.6.0+) -->
<a :[key]="url"> ... </a>
```

#### `v-on` Shorthand <a href="#v-on-shorthand" id="v-on-shorthand"></a>

```javascript
<!-- full syntax -->
<a v-on:click="doSomething"> ... </a>

<!-- shorthand -->
<a @click="doSomething"> ... </a>

<!-- shorthand with dynamic argument (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

