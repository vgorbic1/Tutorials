## How to change the Stare in the render() Method of a Class Component
1. Make sure you actually in the class component.
2. Make sure you have access to the state object.
3. Use `setState()` function that is given with the `Component` extension.
4. `setState()` takes an obbject of the state with the mutated properties.
5. Use an arrow function, otherwise bind this function to the class.
```js
...
render() {
  <div>
    <h1 onClick={ () => this.setState({ counter: 3 }) }>Change State</h1>
...
```
