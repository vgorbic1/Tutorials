## RESTful Applications
REST is not an architecture; rather, it is a set of constraints that creates a software architectural style,
which can be used for building distributed applications.

[Architectural Styles and the Design of Network-Based Software Architectures, Roy
Fielding, 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)

Without any constraints, one may end up
developing applications with no rules or limits that are hard to maintain and extend.

### Set of Constrains:
- **Client-server**: This constraint keeps the client and the server loosely coupled. It means that the
client does not need to know the implementation details in the server and the server is not
worried about how the data is used by the client. However, a common interface is maintained
between the client and the server to ease the communication.
- **Stateless**: There should be no need for the service to keep users' sessions. In other words, each
request should be independent of the others.
- **Cacheable**: The network infrastructure should
support a cache at different levels. Caching can avoid repeated round trips between the client
and the server for retrieving the same resource.
- **Uniform interface**: This constraint indicates a generic interface to manage all interactions
between the client and the server in a unified way, which simplifies and decouples the
architecture. This constraint indicates that each resource exposed for use by the client must have
a unique address and should be accessible through a generic interface. The client can act on the
resources by using a generic set of methods.
- **Layered system**: The server can have multiple layers for implementation. This layered
architecture helps to improve scalability by enabling load balancing. It also improves
performance by providing shared caches at different levels. The top layer, being the door to the
system, can enforce security policies as well.
- **Code on demand**: This constraint is optional. This constraint indicates that the functionality of
the client applications can be extended at runtime by allowing a code download from the server
and executing the code. Some examples are the applets and the JavaScript code that get
transferred and executed on the client side at runtime.

![cc]()

