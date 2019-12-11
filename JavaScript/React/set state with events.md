## Set State with an Event
When changing the state (with `setState()`) with a synthetic event, remember
that `setState` is an asynchronous:
```js
onClick={() => {
  this.setState({name: 'John'});
  console.log(this.state);
}}
```
The console will display the current (not yet new) state, since the `setState` is asynchronous.
### Solution
Set a callback function that is going to run after the `setState` is finished:
```js
onClick={ () => {
  this.setState({name: 'John'}, () => console.log(this.state) );
}}
```
