## Timing Events

JavaScript can be executed in time intervals using mehtods:

#### setInterval
This method waits a specific number of miliseconds and then executes assigned function.
```javascript
setInterval(
  function() {
    alert('hello!')
  }
  , 3000
);
```

#### clearInterval
This method stops execution of the function.
```javascript
clearInterval();
```

#### setTimeout
This method waits the specified time in milliseconds and then execute the function.
```javascript
setTimeout(
  function() {
    alert('hello!')
  }
  , 3000
);  
```

#### clearTimeout
This method stops execution of the function.
```javascript
clearTimeout();
```
