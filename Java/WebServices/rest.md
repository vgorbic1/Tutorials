## RESTful Services

Service-Oriented Architecture (SOA). The SOA is essentially a
collection of services, each talking to one another in a well-defined manner, in order to complete
relatively large and logically complete business processes.

REST is not the system's architecture in itself, but it is a set of constraints that when
applied to the system's design leads to a RESTful architecture.

The RESTful web API or REST API is an API implemented using HTTP and the REST architectural
constraints. Technically speaking, this is just another term for a RESTful web service.

### Resources

A RESTful resource is anything that is addressable over the Web. By addressable, we mean resources
that can be accessed and transferred between clients and servers.

Here are some examples of the REST resources:
- A news story
- The temperature in NY at 4:00 p.m. EST
- A tax return stored in the IRS database
- A list of code revision history in a repository such as SVN or CVS
- A search result for a particular item in a Web index, such as Google

In a RESTful architecture, each resource can be accessed directly and independently, and sometimes, different
requests may point to the same resource.

### URI
A URI is a string of characters used to identify a resource over the Web. In simple words, the URI in a
RESTful web service is a hyperlink to a resource, and it is the only means for clients and servers to
exchange representations.

In a RESTful system, the URI is not meant to change over time as it may break the
contract between a client and a server. More importantly, even if the underlying infrastructure or
hardware changes (for example, swapping the database servers) for a server hosting REST APIs, the
URIs for resources are expected to remain the same as long as the web service is up and running.

### The representation of resources
The representation of resources is what is sent back and forth between clients and servers in a
RESTful system. A representation is a temporal state of the actual data located in some storage
device at the time of a request. In general terms, it is a binary stream together with its metadata that
describes how the stream is to be consumed by the client.

A representation can
take various forms, such as an image, a text file, an XML, or a JSON format. However, all clients
will use the same URI with appropriate Accept header values for accessing the same resource in
different representations.

For the human-generated requests through a web browser, a representation is typically in the form of
an HTML page. For automated requests from the other web services, readability is not as important
and a more efficient representation, such as JSON or XML, can be used.

### Representation of CRUD Methods

Data action | HTTP equivalent
-- | --
CREATE | POST or PUT
READ | GET
UPDATE | PUT or PATCH
DELETE | DELETE

However, RESTful web services are not limited to just these four basic data manipulation
concepts. They can even be used for executing business logic on the server, but remember that every
result must be a resource representation of the domain at hand.

#### GET method

The method, GET, is used to retrieve resources. The HTTP GET method should only be used to retrieve representations, 
not for performing any update on the resource. A GET request must be safe and idempotent. (eye - dem - potent) 
Idempotency is when making multiple identical requests has the same effect as making a single request.

#### The HTTP POST method

The POST method is used to create resources. The 201 "Created" response code with a location URI 
is returned if the operation is successfull.

#### The HTTP PUT method

The PUT method is used to update resources. To update a resource, we first need its representation in
the client; secondly, at the client level, we update the resource with the new value(s) that we want;
and finally, we update the resource by using a PUT request together with the representation as its
payload.

The 204 "No Content" response code indicates that the server has fulfilled the request but does not 
return the entity body.

#### The HTTP DELETE method

The DELETE method is used to delete the resource. The 204 "No Content" response code is returned.

### Hypermedia as the Engine of Application State (HATEOAS)

In a RESTful system, there is no fixed interface between the client and the server as you may see in a
conventional client-server communication model such as Common Object Request Broker
Architecture (CORBA) and Java Remote Method Invocation (Java RMI). With REST, the client
just needs to know how to deal with the hypermedia links present in the response body; next, the call
to retrieve the appropriate resource representation is made by using these dynamic media links. This
concept makes the client-server interaction very dynamic and keeps it different from the other
network application architectures.



## Java tools and frameworks for building RESTful web services

The Java API for RESTful web services is called JAX-RS.
JAX-RS is a part of the Java Platform Enterprise Edition (Java EE).

There are many reference implementations available for JAX-RS today. Some of the most
popular implementations are Jersey, Apache CXF, RESTEasy, and Restlet. At this juncture, it is
worth mentioning that most of the frameworks in the preceding list, such as Jersey and Apache CXF,
are not just limited to reference implementations of the JAX-RS specifications, but they also offer
many additional features on top of the specifications.

Apart from the JAX-RS-based frameworks (or extensions built on top of JAX-RS), one may also find
some promising nonstandard (not based on JAX-RS) Java REST frameworks on the market. Some
such frameworks are as follows:

- RESTX, which is an open source Java REST framework and is
primarily focused on the server-side REST API development. This is relatively new on the
market and simplifies the REST API development.
- Spark is another framework that falls into this category. It is a Java web framework with support
for building REST APIs. Spark 2.0 is built using Java 8, leveraging all the latest improvements
of the Java language.
- Play is another framework worth mentioning in this category. It is a Java (and Scala)-based web
application framework with inherent support for building RESTful web services.


## Java APIs for JSON Processing

XML and JSON are the two most popular formats used by RESTful web services today. Out of these
two formats, JSON has been widely adopted by many vendors because of it is simple and lightweight.

In Java RESTful web service frameworks, such as JAX-RS, for building RESTful web APIs,
the serialization and deserialization of the request and response messages will be taken care of by the
framework.



