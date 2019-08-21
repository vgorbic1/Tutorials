## Errors
Used to test a block of code for errors.

### Throw an Error
```js
throw new Error('error message goes here')
```

### Try and Catch (Synchronous Errors)
Test a code within **try** block and go to **catch** if an error happened.
```javascript
function message() {
  try {
    alert("Hi!");
  } catch(err) {
    alert(err.message);
  }
};
```

### Catch Method (Asynchronous Errors)
#### with promises:
```js
// silent fail:
Promise.resolve('async fail')
  .then(response => {
    throw new Error('#1 fail')
    return response
  })
  .then(response => {
    console.log(response)
  })
  
// with catch method (preferable way):
Promise.resolve('async fail')
  .then(response => {
    throw new Error('#1 fail')
    return response
  })
  .then(response => {
    console.log(response)
  })
  .catch(e => console.log(e))
```
#### with async await:
Use try-catch block
```js
(async function() {
  try {
    await Promise.resolve('Resolved')
    await Promise.reject('Rejected')
  } catch (err) {
    console.log(err);
  }
})()
```
