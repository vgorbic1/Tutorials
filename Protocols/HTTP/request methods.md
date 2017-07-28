## HTTP Request Methods

These are request methods:

 mehtod | description 
 --- | --- 
GET | This method is used for retrieving resources from the server by using the given URI.
HEAD | This method is the same as the GET request, but it only transfers the status line and the header section without the response body.
POST | This method is used for posting data to the server. The server stores the data (entity) as a new subordinate of the resource identified by the URI. If you execute POST multiple times on a resource, it may yield different results.
PUT | This method is used for updating the resource pointed at by the URI. If the URI does not point to an existing resource, the server can create the resource with that URI.
DELETE | This method deletes the resource pointed at by the URI.
TRACE | This method is used for echoing the contents of the received request. This is useful for the debugging purpose with which the client can see what changes (if any) have been made by the intermediate servers.
OPTIONS | This method returns the HTTP methods that the server supports for the specified URI.
CONNECT | This method is used for establishing a connection to the target server over HTTP.
PATCH | This method is used for applying partial modifications to a resource identified by the URI.

