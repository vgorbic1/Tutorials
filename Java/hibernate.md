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



