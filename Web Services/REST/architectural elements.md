## The Core Architectural Elements of a RESTful System

### Resources
A RESTful resource is anything that is addressable over the Web, meaning that resources
can be accessed and transferred between clients and servers.

Resource examples:
- A news story
- The temperature in NY at 4:00 p.m. EST
- A tax return stored in the IRS database
- A list of code revision history in a repository such as SVN or CVS
- A student in a classroom in a school
- A search result for a particular item in a Web index, such as Google

In a RESTful architecture, each resource can be accessed directly and independently, and sometimes, different
requests may point to the same resource.

In a RESTful system, the representation of a resource in the
response body depends on the desired Internet media type, which is specified within the request
header sent by the client.

### URI
A URI is a string of characters used to identify a resource over the Web. In simple words, the URI in a
RESTful web service is a hyperlink to a resource, and it is the only means for clients and servers to
exchange representations.

The client uses a URI to locate the resources over Web and then, sends a request to the server and
reads the response. In a RESTful system, the URI is not meant to change over time as it may break the
contract between a client and a server. More importantly, even if the underlying infrastructure or
hardware changes (for example, swapping the database servers) for a server hosting REST APIs, the
URIs for resources are expected to remain the same as long as the web service is up and running.

### The Representation of Resources
The representation of resources is what is sent back and forth between clients and servers in a
RESTful system. A representation is a temporal state of the actual data located in some storage
device at the time of a request. In general terms, it is a binary stream together with its metadata that
describes how the stream is to be consumed by the client. The metadata can also contain extra
information about the resource, for example, validation, encryption information, or extra code to be
executed at runtime.

Different clients can consume different representations of the same resource. Therefore, a representation can
take various forms, such as an image, a text file, an XML, or a JSON format. However, all clients
will use the same URI with appropriate `Accept` header values for accessing the same resource in
different representations.

For the human-generated requests through a web browser, a representation is typically in the form of
an HTML page. For automated requests from the other web services, readability is not as important
and a more efficient representation, such as JSON or XML, can be used.
