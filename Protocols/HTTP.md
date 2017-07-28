## HTTP
Hypertext Transfer Protocol (HTTP) is the foundation of data communication for World Wide Web.
This protocol defines how messages are formatted, transmitted, and processed over the Internet.

### HTTP Versions
- **HTTP/0.9** was the first documented version, which was released in 1991. This was very primitive and
supported only the GET method.
- **HTTP/1.0** was released in 1996 with more features
and corrections in the previous release. HTTP/1.0 supported more request
methods such as GET, HEAD, and POST. 
- **HTTP/1.1** was instroduced in 1999. This was the
revision of HTTP/1.0. This version is in common use today.
- **HTTP/2** (originally named HTTP 2.0) is the next planned version. It is mainly focused on how the
data is framed and transported between the client and the server.

HTTP works in a request-response manner:
- The user enters the following URL in the browser `http://www.example.com/index.html` and
then submits the request.
- The browser establishes a connection with the server and sends a request to
the server:
```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/htmlAccept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
```
The header fields are colon-separated key-value pairs in the plain-text format,
terminated by a carriage return followed by a line feed character. The server can use this 
information while preparing the response for the
request. A blank line is used at the end of the header to indicate the end of the header portion in a
request. The last part of an HTTP request is the HTTP body. Typically, the body is left blank unless the client
has some data to submit to the server. In this example, the body part is empty as this is a GET request
for retrieving a page from the server.
- Once the server receives the HTTP request, it
will process the message and return a response to the client.
```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: max-age=604800
Content-Type: text/html
Date: Wed, 03 Dec 2014 15:05:59 GMT
Content-Length: 1270

<html>
<head>
<title>An Example Page</title>
</head>
<body>
Hello World !
</body>
</html>
```
The first line in the response is a status line. It contains the HTTP version that the server is using,
followed by a numeric status code and its associated textual phrase.
Similar to the request header, the
response header follows the colon-separated name-value pair format terminated by the carriage
return and line feed characters.
The HTTP response header can contain useful information about the
resource being fetched, the server hosting the resource, and some parameters controlling the client
behavior while dealing with the resource, such as content type, cache expiry, and refresh rate.
The last part of the response is the response body. Upon the successful processing of the request, the
server will add the requested resource in the HTTP response body. It can be HTML, binary data,
image, video, text, XML, JSON, and so on.
- Once the response body has been sent to the requestor, the
HTTP server will disconnect if the connection created during the request is not of the `keep-alive`
type: `Connection: keep-alive` in the header.
