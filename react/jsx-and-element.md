---
description: >-
  It is a syntax extension to JavaScript. JSX produces React “elements”.
  Elements are the smallest building blocks of React apps.
---

# JSX and Element

JSX — Allows us to write HTML like syntax which gets transformed to lightweight JavaScript objects. 

JSX is quite similar to html and can convert html to JSX using online compiler or htmltojsx on npm. 

With our knowledge so far, the only way to update the UI is to create a new element, and pass it to `ReactDOM.render()`.

## Embedding Expressions in JSX

 You can put any valid [JavaScript expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) inside the curly braces in JSX. 

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);
```

## JSX is an Expression Too

You can use JSX inside of `if` statements and `for` loops, assign it to variables, accept it as arguments, and return it from functions:

```jsx
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

## Specifying Attributes with JSX

 You may use quotes to specify string literals as attributes:

```jsx
const element = <div tabIndex="0"></div>;
```

 You may also use curly braces to embed a JavaScript expression in an attribute:

```jsx
const element = <img src={user.avatarUrl}></img>;
```

 Don’t put quotes around curly braces when embedding a JavaScript expression in an attribute. You should either use quotes \(for string values\) or curly braces \(for expressions\), but not both in the same attribute.

## JSX Represents Objects

 Babel compiles JSX down to `React.createElement()` calls.

These two examples are identical:

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```jsx
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

