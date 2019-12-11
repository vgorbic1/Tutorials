## Set State in a Class Component

To set state in a class component do it in the constructor:
```js
import React from 'react';

class App extends React.Component {

  constructor(props) {
    super(props);
    
    this.state = {
      name: 'James',
      counter: 0
    };
  }
  ...
 ```
Now address that state property in any other function of this class:
```js
...
setNewCounter = () => {
    this.setState(state => ({
      ...state,
      counter: 1,
    }));
  }
...
```
Or display it in the `render()`:
```js
...
  render() {
    return (
      <h1>Counter: {this.state.counter}</h1>
    )
  }
...
```
