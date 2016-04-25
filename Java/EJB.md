## Enterprise Java Beans (EJB)
EJB provides an architecture to develop and deploy component based enterprise applications considering robustness, high scalability and high performance.

#### Benefits
* Simplified development of large scale enterprise level application.
* Application Server/ EJB container provides most of the system level services like transaction handling, logging, load balancing, persistence mechanism, exception handling and so on. Developer has to focus only on business logic of the application.
* EJB container manages life cycle of ejb instances thus developer needs not to worry about when to create/delete ejb objects.

#### Disadvantages
* Requires application server.
* Requires only java client. For other language client, you need to go for webservice.
* Complex to understand and develop ejb applications.

#### When use Enterprise Java Bean?
* Application needs Remote Access. In other words, it is distributed.
* Application needs to be scalable. EJB applications supports load balancing, clustering and fail-over.
* Application needs encapsulated business logic. EJB application is separated from presentation and persistent layer.

#### EJB types
EJB are primarily of three types which are briefly described below:
* `Session Bean`.	Session bean stores data of a particular user for a single session. It can be stateful or stateless. It is less resource intensive as compared to entity beans. Session bean gets destroyed as soon as user session terminates.
* `Entity Bean`.	Entity beans represents persistent data storage. User data can be saved to database via entity beans and later on can be retrived from the database in the entity bean.
* `Message Driven Bean`.	Message driven beans are used in context of JMS (Java Messaging Service). Message Driven Beans can consumes JMS messages from external entities and act accordingly.

#### Difference between RMI and EJB.
Both RMI and EJB, provides services to access an object running in another JVM (known as remote object) from another JVM. The differences between RMI and EJB are given below:
* In RMI, middleware services such as security, transaction management, object pooling etc. need to be done by the java programmer.	In EJB, middleware services are provided by EJB Container automatically.
* RMI is not a server-side component. It is not required to be deployed on the server.	EJB is a server-side component, it is required to be deployed on the server.
* RMI is built on the top of socket programming. EJB technology is built on the top of RMI.

In EJB, bean component and bean client both must be written in java language. If bean client need to be written in other language such as .net, php etc, we need to go with webservices (SOAP or REST). So EJB with web service will be better option.

### Session Bean
Session bean encapsulates business logic only, it can be invoked by local, remote and webservice client. It can be used for calculations, database access etc. The life cycle of session bean is maintained by the application server (EJB Container). There are 3 types of session bean.
* Stateless Session Bean: It doesn't maintain state of a client between multiple method calls.
* Stateful Session Bean: It maintains state of a client across multiple requests.
* Singleton Session Bean: One instance per application, it is shared between clients and supports concurrent access.
