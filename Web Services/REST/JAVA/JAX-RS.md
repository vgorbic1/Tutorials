## JAX-RS
The main goal of the JAX-RS specification is to make the RESTful web service development easier
than it has been in the past. As JAX-RS is a part of the Java EE platform, your code becomes portable
across all Java EE-compliant servers.

There are multiple JAX-RS implementations available today by various vendors:
- **Jersey** RESTful web service framework is an open source framework for
developing RESTful web services in Java. It serves as a JAX-RS reference implementation.
[Learn more](https://jersey.java.net) about this project.
- **Apache CXF** is an open source web services framework. CXF supports both
JAX-WS and JAX-RS web services. [Learn more](http://cxf.apache.org) about CXF.
- **RESTEasy** is an open source project from JBoss, which provides various
modules to help you build a RESTful web service. [Learn more](http://resteasy.jboss.org) about RESTEasy.
- **Restlet** is a lightweight, open source RESTful web service framework. It has
good support for building both scalable RESTful web service APIs and lightweight REST
clients, which suits mobile platforms well. [Learn more](http://restlet.com) about Restlet.

### JAX-RS as a Maven Project
To use JAX-RS APIs in your project, you need to add the `javax.ws.rs-api` JAR file to the class
path. If the consuming project uses Maven for building the source, the dependency entry for the
`javax.ws.rs-api` JAR file in the Project Object Model (POM) file may look like the following:
```xml
<dependency>
 <groupId>javax.ws.rs</groupId>
 <artifactId>javax.ws.rs-api</artifactId>
 <version>2.0.1</version><!-- set the tight version -->
 <scope>provided</scope><!-- compile time dependency -->
</dependency>
```

### Annotations
Java annotations provide the metadata for your Java class, which can be used during compilation,
during deployment, or at runtime in order to perform designated tasks. The use of annotations allows
us to create RESTful web services as easily as we develop a POJO class.

#### @Path
The `@javax.ws.rs.Path` annotation indicates the URI path to which a resource class or a class
method will respond. The value that you specify for the @Path annotation is relative to the URI of the
server where the REST resource is hosted. This annotation can be applied at both the class and the
method levels.

A @Path annotation value is not required to have leading or trailing slashes (/), as you may see in
some examples. The JAX-RS runtime will parse the URI path templates in the same way even if they
have leading or trailing slashes.
```java
import javax.ws.rs.Path;
@Path("departments")
  public class DepartmentService {
  // Rest of the code goes here
}
```
```java
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
@Path("departments")
public class DepartmentService {
  @GET
  @Path("count")
  @Produces("text/plain")
  public Integer getTotalDepartments() {
    return findTotalRecordCount();
  }
//Rest of the code goes here
}
```
It is very common that a client wants to retrieve data for a specific object by passing the desired
parameter to the server. JAX-RS allows you to do this via the URI path variables:
```java
import javax.ws.rs.Path;
import javax.ws.rs.DELETE;
@Path("departments")
public class DepartmentService {
  @DELETE
  @Path("{id}")
  public void removeDepartment(@PathParam("id") short id) {
    removeDepartmentEntity(id);
  }
  // Other methods removed for brevity
}
```
JAX-RS lets you use regular expressions in the URI path template for restricting the values set for the
path variables at runtime by the client. By default, the JAX-RS runtime ensures that all the URI
variables match the following regular expression: `[^/]+?`.
```java
@DELETE
@Path("{name: [a-zA-Z][a-zA-Z_0-9]}")
  public void removeDepartmentByName(@PathParam("name") String deptName) {
  // Method implementation goes here
}
```
#### @Produces
The `@javax.ws.rs.Produces` annotation is used for defining the Internet media type(s) that a REST
resource class method can return to the client. You can define this either at the class level (which will
get defaulted for all methods) or the method level. The method-level annotations override the classlevel
annotations. The following example uses the @Produces annotation at the class level in order to set the default
response media type as JSON for all resource methods in this class:
```java
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
@Path("departments")
@Produces(MediaType.APPLICATION_JSON)
public class DepartmentService {
  ...
```
#### @Consumes
The `@javax.ws.rs.Consumes` annotation defines the Internet media type(s) that the resource class
methods can accept. You can define the @Consumes annotation either at the class level (which will get
defaulted for all methods) or the method level. The method-level annotations override the class-level
annotations.
```java
import javax.ws.rs.Consumes;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.POST;
@POST
@Consumes(MediaType.APPLICATION_JSON)
public void createDepartment(Department entity) {
  ...
```
