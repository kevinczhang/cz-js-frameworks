# Life cycle

## **Mounting**

These methods are called in the following order when an instance of a component is being created and inserted into the DOM:

* [constructor\(\)](https://reactjs.org/docs/react-component.html#constructor)
* [static getDerivedStateFromProps\(\)](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
* [render\(\)](https://reactjs.org/docs/react-component.html#render)
* [componentDidMount\(\)](https://reactjs.org/docs/react-component.html#componentdidmount)

## **Updating**

An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered:

* [static getDerivedStateFromProps\(\)](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
* [shouldComponentUpdate\(\)](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)
* [render\(\)](https://reactjs.org/docs/react-component.html#render)
* [getSnapshotBeforeUpdate\(\)](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)
* [componentDidUpdate\(\)](https://reactjs.org/docs/react-component.html#componentdidupdate)

## **Unmounting**

This method is called when a component is being removed from the DOM:

* [componentWillUnmount\(\)](https://reactjs.org/docs/react-component.html#componentwillunmount)

## **Error Handling**

These methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.

* [static getDerivedStateFromError\(\)](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)
* [componentDidCatch\(\)](https://reactjs.org/docs/react-component.html#componentdidcatch)

## Other APIs

Each component also provides some other APIs:

* [setState\(\)](https://reactjs.org/docs/react-component.html#setstate)
* [forceUpdate\(\)](https://reactjs.org/docs/react-component.html#forceupdate)

#### Class Properties

* [defaultProps](https://reactjs.org/docs/react-component.html#defaultprops)
* [displayName](https://reactjs.org/docs/react-component.html#displayname)

#### Instance Properties

* [props](https://reactjs.org/docs/react-component.html#props)
* [state](https://reactjs.org/docs/react-component.html#state)

