## Web Workers

A web worker is a JavaScript code running in the background. The workers are supported by all browsers. (IE 10+)

Check wheather the user's browser supports web workers:
```javascript
if (typeof(Worker) !== 'undefined') {
  // worker goes here
} else {
  // sorry, no support
}
```

#### Creating a Worker
Create a worker is external JavaScript file.
```javascript
var i = 0;
function timedCount(){
  i = i + 1;
  postMessage(i);  // post a message back to HTML page
  setTimeout('timedCount()', 500);
}
timedCount;
```
