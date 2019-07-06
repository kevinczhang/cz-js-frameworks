---
description: >-
  Components let you split the UI into independent, reusable pieces, and think
  about each piece in isolation.
---

# Components and Props

Conceptually, components are like JavaScript functions. They accept arbitrary inputs \(called “props”\) and return React elements describing what should appear on the screen.

## Function Component

Function Component accepts a single “props” \(which stands for properties\) object argument with data and returns a React element. Props are read only.

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

## Class Component

### Overview

1. Class Component: Input: Props and State; Output: React.Component.
2. State can be changed, but Props not.
3. This.setState will trigger the render method.
4. If we export a class using default, like export default component, x; We can Import it without {} and with any name, like import comp, {x} from "./module". Only apply to first exported parameter.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }
  
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
        <button onClick={this.handleClick}>
          Click me
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

### Using State Correctly <a id="using-state-correctly"></a>

#### Do Not Modify State Directly. Use the setState. <a id="do-not-modify-state-directly"></a>

```text
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

#### State Updates are Merged <a id="state-updates-are-merged"></a>

 When you call `setState()`, React merges the object you provide into the current state.

## Preventing Component from Rendering

In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return `null` instead of its render output. 

Returning `null` from a component’s `render` method does not affect the firing of the component’s lifecycle methods. For instance `componentDidUpdate` will still be called.

## Keys

 Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:

```jsx
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

 Keys only make sense in the context of the surrounding array.  Keys used within arrays should be unique among their siblings. However they don’t need to be globally unique. 

