## Errors
Used to test a block of code for errors.

### Throw an Error
```js
throw new Error('error message goes here')
```

### Try and Catch
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
