# Conditional Rendering

## `v-if`

&#x20;The directive `v-if` is used to conditionally render a block. The block will only be rendered if the directive’s expression returns a truthy value.

```markup
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>

<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

&#x20;This isn’t always desirable though, so Vue offers a way for you to say, “These two elements are completely separate - don’t re-use them.” Add a `key` attribute with unique values:

```markup
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

## `v-show`

```markup
<h1 v-show="ok">Hello!</h1>
The difference is that an element with v-show will always be rendered and 
remain in the DOM; v-show only toggles the display CSS property of the element.
```

&#x20;Generally speaking, `v-if` has higher toggle costs while `v-show` has higher initial render costs. So prefer `v-show` if you need to toggle something very often, and prefer `v-if` if the condition is unlikely to change at runtime.
