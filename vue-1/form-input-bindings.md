# Form Input Bindings

&#x20;You can use the `v-model` directive to create two-way data bindings on form input, textarea, and select elements.

`v-model` internally uses different properties and emits different events for different input elements:

* text and textarea elements use `value` property and `input` event;
* checkboxes and radiobuttons use `checked` property and `change` event;
* select fields use `value` as a prop and `change` as an event.

```markup
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>

<span>Multiline message is:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<br>
<textarea v-model="message" placeholder="add multiple lines"></textarea>

<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>

<!--Multiple checkboxes, bound to the same Array:-->
<div id='example-3'>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Checked names: {{ checkedNames }}</span>
</div>

<input type="radio" id="one" value="One" v-model="picked">
<label for="one">One</label>
<br>
<input type="radio" id="two" value="Two" v-model="picked">
<label for="two">Two</label>
<br>
<span>Picked: {{ picked }}</span>

<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selected: {{ selected }}</span>

<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br>
<span>Selected: {{ selected }}</span>
```

&#x20;Dynamic options rendered with `v-for`:

```markup
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
```

```javascript
new Vue({
  el: '...',
  data: {
    selected: 'A',
    options: [
      { text: 'One', value: 'A' },
      { text: 'Two', value: 'B' },
      { text: 'Three', value: 'C' }
    ]
  }
})
```

```markup
<!-- `picked` is a string "a" when checked -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` is either true or false -->
<input type="checkbox" v-model="toggle">

<!-- `selected` is a string "abc" when the first option is selected -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

```markup
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no"
>
// when checked:
vm.toggle === 'yes'
// when unchecked:
vm.toggle === 'no'
```

```markup
<input type="radio" v-model="pick" v-bind:value="a">
// when checked:
vm.pick === vm.a
```

```markup
<select v-model="selected">
  <!-- inline object literal -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
// when selected:
typeof vm.selected // => 'object'
vm.selected.number // => 123
```

```markup
<!-- synced after "change" instead of "input" -->
<input v-model.lazy="msg">
<input v-model.number="age" type="number">
<input v-model.trim="msg">
```
