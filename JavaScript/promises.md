## Promises
A promise is an object that may produce a single value some time int he future. 
Either a resolverd value, or a reason that it's not resolved (rejected)
A promise could be in three possible states:
- fullfilled
- rejected
- pending

Promises are great for asyncronous programming.
### Before Promises it was Callbacks
that could easily become a callback pyramid of doom:
```js
movePlayer(100, function() {
  movePlayer(400, function() {
    movePlayer(10, function() {
      movePlayer(500, function() {
        // do stuff
      });
    });
  });
});
```
Promises serve the same purposes as callbacks, but with cleaner code:
```js
movePlayer(100)
  .then(() => movePlayer(400))
  .then(() => movePlayer(10))
  .then(() => movePlayer(500))
```
### Creating a Promise
```js
const promise = new Promise( (resolve, reject) => {
  if (true) {
    resolve('worked')
  } else {
    reject('broke')
  }
})

promise
  .then(result => result + '!')
  .then(result2 => console.log(result2))
  .catch( () => console.log('error!'))
```
