## Cross-Origin Resource Sharing

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers 
to tell browsers to give a web application running at one origin, access to selected resources 
from a different origin. A web application executes a cross-origin HTTP request when it requests 
a resource that has a **different origin (domain, protocol, or port)** from its own.

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts.
This means that a web application using those APIs can only request resources from the same 
origin the application was loaded from, unless the response from other origins includes the 
right CORS headers.

Modern browsers use CORS in a APIs such as XMLHttpRequest or Fetch to mitigate the risks of 
cross-origin HTTP requests.

### What requests use CORS?
- Invocations of the XMLHttpRequest or Fetch APIs.
- Web Fonts (for cross-domain font usage in @font-face within CSS).
- WebGL textures.
- Images/video frames drawn to a canvas using drawImage().
- CSS Shapes from images.

### Mechanism
The Cross-Origin Resource Sharing standard works by adding new HTTP headers that let servers 
describe which origins are permitted to read that information from a web browser. 
Additionally, for HTTP request methods that can cause side-effects on server data, the specification 
mandates that browsers "preflight" the request, soliciting supported methods from the server with 
the HTTP OPTIONS request method, and then, upon "approval" from the server, sending the actual request. 
Servers can also inform clients whether "credentials" (such as Cookies and HTTP Authentication) 
should be sent with requests.

CORS failures result in errors, but for security reasons, specifics about the error are not available to JavaScript.

### Simple Requests
Some requests don’t trigger a CORS preflight. Those are called **simple requests**:
- GET, HEAD, or POST methods
- Specific [headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#Simple_requests) 
- Specific "ContentType" header [values](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#Simple_requests)

### Access-Control-Allow-Origin
Server sends Access-Control-Allow-Origin response.
```
Access-Control-Allow-Origin: *
```
Means that the resource can be accessed by any domain.

If the resource owners at *https://bar.other* wished to restrict access to the resource to 
requests only from *https://foo.example*, they would send:
```
Access-Control-Allow-Origin: https://foo.example
```

### Preflighted Requests
Unlike **simple requests**, **preflighted** requests first send an HTTP request by the OPTIONS method to the resource 
on the other domain, to determine if the actual request is safe to send.
```js
const xhr = new XMLHttpRequest();
xhr.open('POST', 'https://bar.other/resources/post-here/');
xhr.setRequestHeader('Ping-Other', 'pingpong');
xhr.setRequestHeader('Content-Type', 'application/xml');
xhr.onreadystatechange = handler;
xhr.send('<person><name>Arun</name></person>'); 
```
The example above creates an XML body to send with the POST request. Also, a non-standard HTTP *Ping-Other* request header 
is set. Such headers are not part of HTTP/1.1, but are generally useful to web applications. Since the request uses 
a *Content-Type of application/xml*, and since a custom header is set, this request is preflighted.

### Requests with credentials
By default, in cross-site XMLHttpRequest or Fetch invocations, browsers will not send credentials. A specific flag has to 
be set on the XMLHttpRequest object or the Request constructor when it is invoked.

### The HTTP response headers
[more here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#Access-Control-Allow-Origin)

### Server-Side Access Control
[Server-side PHP Implementation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Server-Side_Access_Control)
