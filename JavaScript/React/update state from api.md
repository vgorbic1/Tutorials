## How to Update the State by Getting Data from API
Use `componentDidMount()` lifecycle function:
```js
...
componentDidMount() {
  fetch('https://jsonplaceholder.typicode.com/users')
  .then(response => response.json())
  .then(users => this.setState({ users }));
}
...
```
When a component mounts (renders on the page) it calls the block of code that
is written in `componentDidMount()`.
