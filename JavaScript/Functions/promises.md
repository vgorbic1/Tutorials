## Promises
A promise is an object that may produce a single value some time in the future. 
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
### Promises with All
To wait untill all promises fullfilled use `all` keyword:
```js
const promise1 = new Promise((resolve, reject) => setTimeout(resolve, 1000, "Hi from promise1"))
const promise2 = new Promise((resolve, reject) => setTimeout(resolvr, 2000, "Hi from promise2"))
const promise3 = new Promise((resolve, reject) => setTimeout(resolvr, 3000, "Hi from promise3"))

Promise.all([promise1, promise2, promise3]).then(console.log(values))
```
### Real Life Example
```
const urls = [
  'https://jsonplaceholder.typicode.com/users',
  'https://jsonplaceholder.typicode.com/posts',
  'https://jsonplaceholder.typicode.com/comments'
]

Promise.all(urls.map(url => {
  return fetch(url).then(response => response.json())
}).then(results => {
  console.log(results[0])
  console.log(results[1])
  console.log(results[2])
}).catch(() => console.log(error))
```
### Previous with Async Await
```js
const urls = [
  'https://jsonplaceholder.typicode.com/users',
  'https://jsonplaceholder.typicode.com/posts',
  'https://jsonplaceholder.typicode.com/comments'
]

const getData = async function() {
  try {
    const [users, posts, comments] = await Promise.all(urls.map(url => {
      return fetch(url).then(response => response.json())
    }).then(results => {
      console.log(users)
      console.log(posts)
      console.log(albums)
    })
  } catch(error) {
     console.log(error)
  }
}
```
