## Node.js
Server-side JavaScript.
#### Simple Node.js application
A dummy html page on server:
```html
<h1>some dummy data should go in here</h1>
<ul>
  <li>walk the dog</li>
  <li>feed the dog</li>
  <li>talk about the NFL draft</li>
</ul>
```
Server-side Node.js code:
```javascript
//Querystring parameters
var fs = require("fs");
var http = require("http");
var url = require("url");

http.createServer(function(request, response) {
  response.writeHead(200);
  var querystring = url.parse(request.url, true).query;
  //console.log(querystring);

  response.write("welcome " + querystring.name);
  response.end();
}).listen(80);

console.log("listening on port 80...");
```
another server-side Node.js file:
```javascript
var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200); //HTTP OK
  //response.write("cubs stink");
  var fs = require("fs"); //fs = filestream
  fs.readFile("dummy.html", "utf8", function(err, data) {
    response.write(data);
    response.end();
  })

}).listen(80);

console.log("listening on port 80....");
```
