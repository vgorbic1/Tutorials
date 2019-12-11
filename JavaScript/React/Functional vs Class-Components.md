## Functional vs Class-Components
The simplest way to define a component in React is to write a JavaScript function.
It’s just a function which accepts props and returns a React element:
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
But you can also use the ES6 class syntax to write components:
```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
Both versions are equivalent and will give you the exact same output.
Now you might ask yourself: *“When should I use a function and when a class?”*

The most obvious one difference is the syntax. A functional component is just a 
plain JavaScript function which accepts props as an argument and returns a React element.

A class component requires you to extend from `React.Component` and create a render function 
which returns a React element. This requires more code but will also give you some 
benefits which you will see later on.

### State
You can now use the `useState` hook to use state in your functional components, but before
it was impossible to use `setState()` in a functional component. This is functional components
somtimes get called **stateless components**.

### Lifecycle Functions
You can now use the `useEffect` hook to use lifecycle events in your functional components,
but before you had no access to these functions, since all lifecycle hooks are coming from 
the `React.Component` which you extend from only in class components.

### Conclusion
And so to answer our question before, you should use functional components if you are writing 
a presentational component which doesn’t have its own state or needs to access a lifecycle hook. 
Otherwise you can stick to class components.
