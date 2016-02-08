## Hibernate
Hibernate is a high-performance Object/Relational persistence and query service which is licensed under the open source GNU Lesser 
General Public License (LGPL) and is free to download. Hibernate not only takes care of the mapping from Java classes to database 
tables (and from Java data types to SQL data types), but also provides data query and retrieval facilities. 
Hibernate is an Object-Relational Mapping (ORM) solution for JAVA and it raised as an open source persistent framework created 
by Gavin King in 2001. Hibernate sits between traditional Java objects and database server to handle all the work in persisting 
those objects based on the appropriate O/R mechanisms and patterns:

![hibernate](https://cloud.githubusercontent.com/assets/13823751/12888493/15eb4262-ce40-11e5-9040-6ce2d2005243.jpg)
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


Hibernate uses various existing Java APIs, like JDBC, Java Transaction API(JTA), and Java Naming and Directory Interface (JNDI). JDBC provides a rudimentary level of abstraction of functionality common to relational databases, allowing almost any database with a JDBC driver to be supported by Hibernate. JNDI and JTA allow Hibernate to be integrated with J2EE application servers. 

**Configuration Object**

The Configuration object is the first Hibernate object you create in any Hibernate application and usually created only once during application initialization. It represents a configuration or properties file required by the Hibernate. The Configuration object provides two keys components:
-	Database Connection: This is handled through one or more configuration files supported by Hibernate. These files are hibernate.properties and hibernate.cfg.xml.
-	Class Mapping Setup: This component creates the connection between the Java classes and database tables.


