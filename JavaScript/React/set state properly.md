## Set State the Proper Way
Since `setState` function is asynchronous, React does not guaranty that the current state will be updated right away:
```js
...
setNewCounter = () => {
    this.setState( {counter: this.state.counter + 1} );
  }
...
```
React rule is to use special function around the state object:
```js
...
setNewCounter = () => {
    this.setState( (prevState, prevProps) => ({counter: prevState.counter + 1});
  }
...
```
If we do not use `this.state` in the `setState`, we can pass the state object:
'```js
...
setNewCounter = () => {
    this.setState( {counter: 2} );
  }
...
```
