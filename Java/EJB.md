## Enterprise Java Beans (EJB)
EJB provides an architecture to develop and deploy component based enterprise applications considering robustness, high scalability and high performance.

#### Benefits
* Simplified development of large scale enterprise level application.
* Application Server/ EJB container provides most of the system level services like transaction handling, logging, load balancing, persistence mechanism, exception handling and so on. Developer has to focus only on business logic of the application.
* EJB container manages life cycle of ejb instances thus developer needs not to worry about when to create/delete ejb objects.

#### EJB types
EJB are primarily of three types which are briefly described below:
* `Session Bean`.	Session bean stores data of a particular user for a single session. It can be stateful or stateless. It is less resource intensive as compared to entity beans. Session bean gets destroyed as soon as user session terminates.
* `Entity Bean`.	Entity beans represents persistent data storage. User data can be saved to database via entity beans and later on can be retrived from the database in the entity bean.
* `Message Driven Bean`.	Message driven beans are used in context of JMS (Java Messaging Service). Message Driven Beans can consumes JMS messages from external entities and act accordingly.

