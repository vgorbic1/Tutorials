## HTTP Status Codes

For every HTTP request, the server returns a status code indicating the processing status of the
request:

`1xx Informational`: This series of status codes indicates informational content. This means
that the request is received and processing is going on:

- `100 Continue`: This code indicates that the server has received the request header and the
client can now send the body content. In this case, the client first makes a request (with the
Expect: 100-continue header) to check whether it can start with a partial request. The
server can then respond either with `100 Continue (OK)` or `417 Expectation Failed
(No)` along with an appropriate reason.
- `101 Switching Protocols`: This code indicates that the server is OK for a protocol
switch request from the client.
- `102 Processing`: This code is an informational status code used for long running
processing to prevent the client from timing out. This tells the client to wait for the future
response, which will have the actual response body.

`2xx Success`: This series of status codes indicates the successful processing of requests:
- `200 OK`: This code indicates that the request is successful and the response content is
returned to the client as appropriate.
- `201 Created`: This code indicates that the request is successful and a new resource is
created.
- `204 No Content`: This code indicates that the request is processed successfully, but there's
no return value for this request. For instance, you may find such status codes in response to
the deletion of a resource.

`3xx Redirection`: This series of status codes indicates that the client needs to perform further
actions to logically end the request:
- `304 Not Modified`: This status indicates that the resource has not been modified since it
was last accessed. This code is returned only when allowed by the client via setting the
request headers as `If-Modified-Since` or `If-None-Match`. The client can take
appropriate action on the basis of this status code.

`4xx Client Error`: This series of status codes indicates an error in processing the request:
- `400 Bad Request`: This code indicates that the server failed to process the request
because of the malformed syntax in the request. The client can try again after correcting the
request.
- `401 Unauthorized`: This code indicates that authentication is required for the resource.
The client can try again with the appropriate authentication.
- `403 Forbidden`: This code indicates that the server is refusing to respond to the request
even if the request is valid. The reason will be listed in the body content if the request is
not a HEAD method.
- `404 Not Found`: This code indicates that the requested resource is not found at the location
specified in the request.
- `405 Method Not Allowed`: This code indicates that the HTTP method specified in the
request is not allowed on the resource identified by the URI.
- `408 Request Timeout`: This code indicates that the client failed to respond within the
time frame set on the server.
- `409 Conflict`: This code indicates that the request cannot be completed because it
conflicts with some rules established on resources, such as validation failure.

`5xx Server Error`: This series of status codes indicates server failures while processing a
valid request. Here is one of the frequently used status codes in this class:
- `500 Internal Server Error`: This code indicates a generic error message, and it tells
that an unexpected error occurred on the server and the request cannot be fulfilled.

The [complete list](http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)
of HTTP status codes maintained by IANA.
