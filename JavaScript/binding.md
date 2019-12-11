## Handle Binding in Class Components
A class component extends `React.Component`, which has functions that we may use
in our class. Such as `render()` or a lifecycle hook `componentDidMount`. In those
functions (methods) the `this` keyword is already binded to the class (via
constructor's `super()`).

To create our own functions (methods) in a class component we need to define, what
context the `this` keyword belongs to. By default JavaScript does not define `this`
context within functions.

### Solutions:
Define `this` scope in the constructor of the class component with `bind()` function 
that takes constructor's `this` reference and applyies it to the function's `this`: 
```js
...
constructor() {
    super();
    this.state = {
      users: []
    };
    this.myFunction = this.myFunction.bind(this);
  }
...
function myFunction() {
  this.setState({ user: 'John' } );
}
...
```
or just use an ES6 arrow function (they are lexical scopped) to set context of `this` 
to whatever context the function was declared:
```js
...
myFunction = () => {
  this.setState({ user: 'John' } );
}
...
```
A good rule of thumb is this: Use arrow functions on any class methods you define and aren't 
part of React (i.e. `render()`, `componentDidMount()`).
