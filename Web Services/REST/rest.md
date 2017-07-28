## RESTful Web Services
REST stands for REpresentational State Transfer. REST is web standards based architecture and uses HTTP Protocol for data communication. It revolves around resource where every component is a resource and a resource is accessed by a common interface using HTTP standard methods. REST was first introduced by Roy Fielding in 2000. 

In REST architecture, a REST Server simply provides access to resources and REST client accesses and presents the resources. Here each resource is identified by URIs/ global IDs. REST uses various representations to represent a resource like text, JSON and XML. Now a days JSON is the most popular format being used in web services.

#### HTTP Methods
Following well known HTTP methods are commonly used in REST based architecture.
* GET - Provides a read only access to a resource.
* PUT - Used to create a new resource.
* DELETE - Used to remove a resource.
* POST - Used to update a existing resource or create a new resource.
* OPTIONS - Used to get the supported operations on a resource.

Here are important points to be considered:
GET operations are read only and are safe. PUT and DELETE operations are idempotent means their result will always same no matter how many times these operations are invoked. PUT and POST operation are nearly same with the difference lying only in the result where PUT operation is idempotent and POST operation can cause different result.

#### Environment Setup
Jersey framework implements JAX-RS 2.0 API, which is standard specification to create RESTful web services. 
* Download the latest version of Jersey framework binaries from [here](https://jersey.java.net/download.html) Make sure you set your CLASSPATH variable on this directory properly otherwise you will face problem while running your application.
* Add Jersey Framework and its dependencies (libraries). Copy all jars from following directories of download jersey zip folder in `WEB-INF/lib` directory of the project.
* 

#### Resources
REST architecture treats every content as a resource. These resources can be text files, html pages, images, videos or dynamic business data. REST Server simply provides access to resources and REST client accesses and modifies the resources. A resource in REST is similar Object in Object Oriented Programming or similar to Entity in a Database. While designing a system, the first thing to do is identify the resources and determine how they are related to each other. Once a resource is identified then its representation is to be decided using a standard format so that server can send the resource in above said format and client can understand the same format.

For example, in the following RESTful Web Services, User is a resource, which is represented using following XML format:
```xml
<user>
   <id>1</id>
   <name>Mahesh</name>
   <profession>Teacher</profession>
</user>
```
Same resource can be represented in JSON format as follows:
```javascript
{
   "id":1,
   "name":"Mahesh",
   "profession":"Teacher"
}
```
REST does not impose any restriction on the format of a resource representation. A client can ask for JSON representation where as another client may ask for XML representation of same resource to the server and so on. It is responsibility of the REST server to pass the client the resource in the format that client understands.
* Both Server and Client should be able to understand and utilize the representation format of the resource.
* Format should be able to represent a resource completely. For example, a resource can contain another resource. Format should be able to represent simple as well as complex structures of resources.
* A resource can have a linkage to another resource, a format should be able to handles such situations.

#### Messages
A client sends a message in form of a HTTP Request and server responds in form of a HTTP Response. This technique is termed as Messaging. These messages contain message data and metadata i.e. information about message itself:
![message](https://cloud.githubusercontent.com/assets/13823751/13498043/df6b0222-e11d-11e5-9598-9d204de18298.jpg)
A sample POST request:
```
POST http://MyService/Person/
Host: MyService
Content-Type: text/xml; charset=utf-8
Content-Length: 123
<?xml version="1.0" encoding="utf-8"?>
<Person>
  <ID>1</ID>
  <Name>M Vaqqas</Name>
  <Email>m.vaqqas@gmail.com</Email>
  <Country>India</Country>
</Person>
```


#### Addressing
Addressing refers to locating a resource or multiple resources lying on the server. It is analogous to locate a postal address of a person. Each resource in REST architecture is identified by its URI, Uniform Resource Identifier. A RESTful service uses a directory hierarchy like human readable URIs to address its resources. A URI is of following format:
```
<protocol>://<service-name>/<ResourceType>/<ResourceID>
```
Purpose of an URI is to locate a resource(s) on the server hosting the web service. Another important attribute of a request is VERB which identifies the operation to be performed on the resource.

Following are important points to be considered while designing a URI:
* Use Plural Noun - Use plural noun to define resources. For example, we've used users to identify users as a resource.
* Avoid using spaces - Use underscore(_) or hyphen(-) when using a long resource name, for example, use `authorized_users` instead of `authorized%20users`.
* Use lowercase letters - Although URI is case-insensitive, it is good practice to keep url in lower case letters only.
* Maintain Backward Compatibility - As Web Service is a public service, a URI once made public should always be available. In case, URI gets updated, redirect the older URI to new URI using HTTP Status code, 300.
* Use HTTP Verb - Always use HTTP Verb like GET, PUT, and DELETE to do the operations on the resource. It is not good to use operations names in URI.

Following is an example of a good URI to fetch a user:
```
http://localhost:8080/UserManagement/rest/UserService/users/1
```
**Query Parameters in URI**

The preceding URI is constructed with the help of a query parameter:
```
http://MyService/Persons?id=1
```
The query parameter approach works just fine and REST does not stop you from using query parameters. However, this approach has a few disadvantages:
* Increased complexity and reduced readability, which will increase if you have more parameters.
* Search-engine crawlers and indexers like Google ignore URIs with query parameters. If you are developing for the Web, this would be a great disadvantage as a portion of your Web service will be hidden from the search engines.

The basic purpose of query parameters is to provide parameters to an operation that needs the data items. For example, if you want the format of the presentation to be decided by the client. You can achieve that through a parameter like this:
```
http://MyService/Persons/1?format=xml&encoding=UTF8
```
or
```
http://MyService/Persons/1?format=json&encoding=UTF8
```
Including the parameters format and encoding here in the main URI in a parent-child hierarchy will not be logically correct as they have no such relation:
```
http://MyService/Persons/1/json/UTF8
```
Query parameters also allow optional parameters. This is not otherwise possible in a URI. You should use query parameters only for the use they are intended for: providing parameter values to a process.

#### Security
Following are the best practices to be followed while designing a RESTful web service.
* Validation - Validate all inputs on the server. Protect your server against SQL or NoSQL injection attacks.
* Session based authentication - Use session based authentication to authenticate a user whenever a request is made to a Web Service method.
* No sensitive data in URL - Never use username, password or session token in URL , these values should be passed to Web Service via POST method.
* Restriction on Method execution - Allow restricted use of methods like GET, POST, DELETE. GET method should not be able to delete data.
* Validate Malformed XML/JSON - Check for well formed input passed to a web service method.
* Throw generic Error Messages - A web service method should use HTTP error messages like 403 to show access forbidden etc.

#### JAX-RS
JAX-RS stands for JAVA API for RESTful Web Services. JAX-RS is a JAVA based programming language API and specification to provide support for created RESTful Webservices.

[SOURCE](http://www.tutorialspoint.com/restful/index.htm)
