# Class

## Overview

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

### Using State Correctly  <a href="#using-state-correctly" id="using-state-correctly"></a>

#### Do Not Modify State Directly. Use the setState.  <a href="#do-not-modify-state-directly" id="do-not-modify-state-directly"></a>

```
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

#### State Updates are Merged  <a href="#state-updates-are-merged" id="state-updates-are-merged"></a>

When you call `setState()`, React merges the object you provide into the current state.

## Preventing Component from Rendering

In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return `null` instead of its render output.

Returning `null` from a component’s `render` method does not affect the firing of the component’s lifecycle methods. For instance `componentDidUpdate` will still be called.
