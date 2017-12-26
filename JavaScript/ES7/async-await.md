## Async and Await Calls
The async function declaration defines an asynchronous function, which returns an AsyncFunction object. Used for asynchronous calls.

### Working Example
```javascript
async function getUsers() {
  // await response of the fetch call
  const response = await fetch('https://jsonplaceholder.typicode.com/users');

  // Only proceed once its resolved
  const data = await response.json();

  // only proceed once second promise is resolved
  return data;
}

getUsers().then(users => console.log(users));
```
Thanks to [Brad Traversy](https://traversymedia.com).
