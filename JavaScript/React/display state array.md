## How to display an array located in the State?

### State

```js
...
this.state = {
  users: [
    { name: 'Peter', id: 1 },
    { name: 'John', id: 2 },
    { name: 'James', id: 3 }
  ]
};
...
```
### Render
Use map() to render the state array:
```js
...
render() {
  return (
    <div>
    { this.users.map( user => (
        <h1 key={user.id}>{user.name}</h1>
      ) ) } 
...
</div>
```
Anytime you use the `map()` function inside of render, or you have a list of the same jsx 
elements one after another, they need a `key` attribute (and CRA will warn you about it if you miss it).
