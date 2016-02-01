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
Create a worker is external JavaScript file:
```javascript
var i = 0;
function timedCount(){
  i = i + 1;
  postMessage(i);  // post a message back to HTML page
  setTimeout('timedCount()', 500);
}
timedCount();
```

Create a Web worker object:
We have to cal the worker file from the HTML page:
```javascript
if (typeof(w) == "undefined") {
  w = new Worker("file.js");
}
```
Check if the worker is already exists. If not, create a new worker object and run the code in file.js

Receive and Send messages to worker:
```javascript
w.onmessage = function(event) {
  documnent.getElementById('result').innerHTML = event.data;
};
```
When the Web worker posts a message, the code within the event listener is excluded. The data from the worker is stored in `event.data`.

To terminate worker:
```javascript
w.terminate();
```
The Web worker object runs until it is teminated!
