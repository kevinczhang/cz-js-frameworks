---
description: >-
  Function Component accepts a single “props” (which stands for properties)
  object argument with data and returns a React element. Props are read only.
---

# Function

## Function Component

```jsx
// Simple way
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
// Use an ES6 class to define a component:
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
// Render the above component
const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
