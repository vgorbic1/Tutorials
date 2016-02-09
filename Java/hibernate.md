## Hibernate
Hibernate is a high-performance Object/Relational persistence and query service which is licensed under the open source GNU Lesser 
General Public License (LGPL) and is free to download. Hibernate not only takes care of the mapping from Java classes to database 
tables (and from Java data types to SQL data types), but also provides data query and retrieval facilities. 
Hibernate is an Object-Relational Mapping (ORM) solution for JAVA and it raised as an open source persistent framework created 
by Gavin King in 2001. Hibernate sits between traditional Java objects and database server to handle all the work in persisting 
those objects based on the appropriate O/R mechanisms and patterns:

![hibernate](https://cloud.githubusercontent.com/assets/13823751/12891458/b26c4606-ce4d-11e5-80d4-27b9cd098848.jpg)
#### JDBC
JDBC stands for Java Database Connectivity and provides a set of Java API for accessing the relational databases from Java program.

**Pros of JDBC:**	
-	Clean and simple SQL processing
- Good performance with large data
- Very good for small applications
- Simple syntax so easy to learn

**Cons of JDBC:**
- Complex if it is used in large projects
- Large programming overhead
- No encapsulation
- Hard to implement MVC concept
- Query is DBMS specific

#### ORM
ORM stands for Object-Relational Mapping (ORM) is a programming technique for converting data between relational databases and object oriented programming languages such as Java, C# etc. When we work with an object-oriented systems, there's a mismatch between the object model and the relational database. RDBMSs represent data in a tabular format whereas object-oriented languages, such as Java or C# represent it as an interconnected graph of objects. 

**ORM Advantages:**
-	Lets business code access objects rather than DB tables.
-	Hides details of SQL queries from OO logic.
-	Based on JDBC 'under the hood'
-	No need to deal with the database implementation.
-	Entities based on business concepts rather than database structure.
-	Transaction management and automatic key generation.
-	Fast development of application.

**ORM Solutions:**
- An API to perform basic CRUD operations on objects of persistent classes.
- A language or API to specify queries that refer to classes and properties of classes.
-	A configurable facility for specifying mapping metadata.
-	A technique to interact with transactional objects to perform dirty checking, lazy association fetching, and other optimization functions.

A persistent framework is an ORM service that stores and retrieves objects into a relational database.

**Hibernate Advantages:**
-	Hibernate takes care of mapping Java classes to database tables using XML files and without writing any line of code.
-	Provides simple APIs for storing and retrieving Java objects directly to and from the database.
-	If there is change in Database or in any table then the only need to change XML file properties.
-	Abstract away the unfamiliar SQL types and provide us to work around familiar Java Objects.
-	Hibernate does not require an application server to operate.
-	Manipulates Complex associations of objects of your database.
-	Minimize database access with smart fetching strategies.
-	Provides Simple querying of data.

**Supported Databases:**
-	HSQL Database Engine
-	DB2/NT
-	MySQL
-	PostgreSQL
-	FrontBase
-	Oracle
-	Microsoft SQL Server Database
-	Sybase SQL Server
-	Informix Dynamic Server

**Supported Technologies:**
-	Hibernate supports a variety of other technologies, including the following:
-	XDoclet Spring
-	J2EE
-	Eclipse plug-ins
-	Maven

#### Architecture
Detailed view of the Hibernate Application Architecture with few important core classes:

![hibernate-2](https://cloud.githubusercontent.com/assets/13823751/12891461/b6787b2a-ce4d-11e5-868f-265c9231e06e.jpg)

Hibernate uses various existing Java APIs, like JDBC, Java Transaction API(JTA), and Java Naming and Directory Interface (JNDI). JDBC provides a rudimentary level of abstraction of functionality common to relational databases, allowing almost any database with a JDBC driver to be supported by Hibernate. JNDI and JTA allow Hibernate to be integrated with J2EE application servers. 

**Configuration Object**

The Configuration object is the first Hibernate object you create in any Hibernate application and usually created only once during application initialization. It represents a configuration or properties file required by the Hibernate. The Configuration object provides two keys components:
-	Database Connection: This is handled through one or more configuration files supported by Hibernate. These files are hibernate.properties and hibernate.cfg.xml.
-	Class Mapping Setup: This component creates the connection between the Java classes and database tables.

**SessionFactory Object**
Configuration object is used to create a SessionFactory object which inturn configures Hibernate for the application using the supplied configuration file and allows for a Session object to be instantiated. The SessionFactory is a thread safe object and used by all the threads of an application. The SessionFactory is heavyweight object so usually it is created during application start up and kept for later use. You would need one SessionFactory object per database using a separate configuration file. So if you are using multiple databases then you would have to create multiple SessionFactory objects.

**Transaction Object**
A Transaction represents a unit of work with the database and most of the RDBMS supports transaction functionality. Transactions in Hibernate are handled by an underlying transaction manager and transaction (from JDBC or JTA). This is an optional object and Hibernate applications may choose not to use this interface, instead managing transactions in their own application code.

**Query Object**
Query objects use SQL or Hibernate Query Language (HQL) string to retrieve data from the database and create objects. A Query instance is used to bind query parameters, limit the number of results returned by the query, and finally to execute the query.

**Criteria Object**
Criteria object are used to create and execute object oriented criteria queries to retrieve objects.

#### Configuration
Hibernate requires to know in advance where to find the mapping information that defines how your Java classes relate to the database tables. Hibernate also requires a set of configuration settings related to database and other related parameters. All such information is usually supplied as a standard Java properties file called hibernate.properties, or as an XML file named hibernate.cfg.xml.

#### FAQ
1 What is ORM?

ORM stands for object/relational mapping. ORM is the automated persistence of objects in a Java application to the tables in a relational database.

2 What does ORM consists of?

An ORM solution consists of the followig four pieces:
- API for performing basic CRUD operations
- API to express queries refering to classes
- Facilities to specify metadata
- Optimization facilities: dirty checking, lazy associations fetching

3. What are the ORM levels ?

The ORM levels are:
- Pure relational (stored procedure)
- Light objects mapping (JDBC)
- Medium object mapping
- Full object Mapping (composition, inheritance, polymorphism, persistence by reachability)

4. What is Hibernate?

Hibernate is a pure Java object-relational mapping (ORM) and persistence framework that allows you to map plain old Java objects to relational database tables using (XML) configuration files. Its purpose is to relieve the developer from a significant amount of relational data persistence-related programming tasks.

5. Why do you need ORM tools like hibernate?

The main advantage of ORM like hibernate is that it shields developers from messy SQL.

6. What Does Hibernate Simplify?

- Saving and retrieving your domain objects
- Making database column and table name changes
- Centralizing pre save and post retrieve logic
- Complex joins for retrieving related items
- Schema creation from object model

7. What is the need for Hibernate xml mapping file?

Hibernate mapping file tells Hibernate which tables and columns to use to load and store objects.

8. What are the Core interfaces are of Hibernate framework?
 
The five core interfaces are used in just about every Hibernate application. Using these interfaces, you can store and retrieve persistent objects and control transactions.
- Session interface
- SessionFactory interface
- Configuration interface
- Transaction interface
- Query and Criteria interfaces

9. What role does the Session interface play in Hibernate?

The Session interface is the primary interface used by Hibernate applications. It is a single-threaded, short-lived object representing a conversation between the application and the persistent store. It allows you to create query objects to retrieve persistent objects. `Session session = sessionFactory.openSession();`

Session interface role:
- Wraps a JDBC connection
- Factory for Transaction
- Holds a mandatory (first-level) cache of persistent objects, used when navigating the object graph or looking up objects by identifier

10. What role does the SessionFactory interface play in Hibernate?

The application obtains Session instances from a SessionFactory. There is typically a single SessionFactory for the whole applicationå¹¼reated during application initialization. The SessionFactory caches generate SQL statements and other mapping metadata that Hibernate uses at runtime. It also holds cached data that has been read in one unit of work and may be reused in a future unit of work `SessionFactory sessionFactory = configuration.buildSessionFactory();`

11. What is the general flow of Hibernate communication with RDBMS?

The general flow of Hibernate communication with RDBMS is:
- Load the Hibernate configuration file and create configuration object. It will automatically load all hbm mapping files
- Create session factory from configuration object
- Get one session from this session factory
- Create HQL Query
- Execute query to get list containing Java objects

12. What is Hibernate Query Language (HQL)?

Hibernate offers a query language that embodies a very powerful and flexible mechanism to query, store, update, and retrieve objects from a database. This language, the Hibernate query Language (HQL), is an object-oriented extension to SQL.

13. How do you map Java Objects with Database tables?
- First we need to write Java domain objects (beans with setter and getter).
- Write hbm.xml, where we map java class to table and database columns to Java class variables.

*SOURCE: [developersbook.com](http://www.developersbook.com/hibernate/interview-questions/hibernate-interview-questions-faqs.php)
