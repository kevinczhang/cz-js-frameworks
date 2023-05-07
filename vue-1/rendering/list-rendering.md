# List Rendering

## With Array

```markup
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

```javascript
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

## With Object

&#x20;You can also use `v-for` to iterate through the properties of an object.

```markup
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

```javascript
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```

You can also provide a second argument for the property’s name (a.k.a. key):

```markup
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```

&#x20;To give Vue a hint so that it can track each node’s identity, and thus reuse and reorder existing elements, you need to provide a unique `key` attribute for each item:

```markup
<div v-for="item in items" v-bind:key="item.id">
  <!-- content -->
</div>
```

&#x20;It is recommended to provide a `key` attribute with `v-for` whenever possible, unless the iterated DOM content is simple, or you are intentionally relying on the default behavior for performance gains.

## Array Change Detection



Vue wraps an observed array’s mutation methods so they will also trigger view updates. The wrapped methods are:

* `push()`
* `pop()`
* `shift()`
* `unshift()`
* `splice()`
* `sort()`
* `reverse()`

&#x20;Mutation methods, as the name suggests, mutate the original array they are called on. In comparison, there are also non-mutating methods, e.g. `filter()`, `concat()` and `slice()`, which do not mutate the original array but **always return a new array**. When working with non-mutating methods, you can replace the old array with the new one:

```javascript
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

## `v-for` with a Range

```markup
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```

### `v-for` on a `<template>` <a href="#v-for-on-a-lt-template-gt" id="v-for-on-a-lt-template-gt"></a>

```markup
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

