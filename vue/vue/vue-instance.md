# Vue Instance

 Every Vue application starts by creating a new **Vue instance** with the `Vue` function:

```javascript
var vm = new Vue({
  // options
})
```

 A Vue application consists of a **root Vue instance** created with `new Vue`, optionally organized into a tree of nested, reusable components.

## [Data and Methods](https://vuejs.org/v2/guide/instance.html#Data-and-Methods)

 When a Vue instance is created, it adds all the properties found in its `data` object to Vue’s **reactivity system**. When the values of those properties change, the view will “react”, updating to match the new values.

 When this data changes, the view will re-render. It should be noted that properties in `data` are only **reactive** if they existed when the instance was created. 

1. If you add a new property b after creation,   changes to `b` will not trigger any view updates.
2.  The only exception to this being the use of `Object.freeze()`, which prevents existing properties from being changed, which also means the reactivity system can’t _track_ changes.

 In addition to data properties, Vue instances expose a number of useful instance properties and methods. These are prefixed with `$` to differentiate them from user-defined properties.

```javascript
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch is an instance method
vm.$watch('a', function (newValue, oldValue) {
  // This callback will be called when `vm.a` changes
})
```

## [Instance Lifecycle Hooks](https://vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks)

Each Vue instance goes through a series of initialization steps when it’s created - for example, it needs to set up data observation, compile the template, mount the instance to the DOM, and update the DOM when data changes.  Along the way, it also runs functions called **lifecycle hooks**, giving users the opportunity to add their own code at specific stages.

```javascript
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` points to the vm instance
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

### [Lifecycle Diagram](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram) <a id="Lifecycle-Diagram"></a>

![](../../.gitbook/assets/image%20%282%29.png)

