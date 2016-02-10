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

A **persistent framework** is an ORM service that stores and retrieves objects into a relational database.

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

**Hibernate Properties:**

- *hibernate.dialect* This property makes Hibernate generate the appropriate SQL for the chosen database.
- *hibernate.connection.driver_class* The JDBC driver class.
- *hibernate.connection.url* The JDBC URL to the database instance.
- *hibernate.connection.username* The database username.
- *hibernate.connection.password* The database password.
- *hibernate.connection.pool_size* Limits the number of connections waiting in the Hibernate database connection pool.
- *hibernate.connection.autocommit* Allows autocommit mode to be used for the JDBC connection.

#### Sessions
A Session is used to get a physical connection with a database. The Session object is lightweight and designed to be instantiated each time an interaction is needed with the database. Persistent objects are saved and retrieved through a Session object. The session objects should not be kept open for a long time because they are not usually thread safe and they should be created and destroyed them as needed. The main function of the Session is to offer create, read and delete operations for instances of mapped entity classes. Instances may exist in one of the following three states at a given point in time:
- **transient**: A new instance of a a persistent class which is not associated with a Session and has no representation in the database and no identifier value is considered transient by Hibernate.
- **persistent**: You can make a transient instance persistent by associating it with a Session. A persistent instance has a representation in the database, an identifier value and is associated with a Session.
- **detached**: Once we close the Hibernate Session, the persistent instance will become a detached instance.

A Session instance is serializable if its persistent classes are serializable. A typical transaction should use the following idiom:
```java
Session session = factory.openSession();
Transaction tx = null;
try {
   tx = session.beginTransaction();
   // do some work
   ...
   tx.commit();
}
catch (Exception e) {
   if (tx!=null) tx.rollback();
   e.printStackTrace(); 
}finally {
   session.close();
}
```
If the Session throws an exception, the transaction must be rolled back and the session must be discarded.

There are number of methods provided by the Session interface. 

#### Persistent Class
Java classes whose objects or instances will be stored in database tables are called persistent classes in Hibernate. Hibernate works best if these classes follow some simple rules, also known as the Plain Old Java Object (POJO) programming model. The POJO name is used to emphasize that a given object is an ordinary Java Object, not a special object, and in particular not an Enterprise JavaBean.
There are following main rules of persistent classes, however, none of these rules are hard requirements.
- All Java classes that will be persisted need a default constructor.
- All classes should contain an ID in order to allow easy identification of your objects within Hibernate and the database. This property maps to the primary key column of a database table.
- All attributes that will be persisted should be declared private and have getters an setters defined in the JavaBean style.
- A central feature of Hibernate, proxies, depends upon the persistent class being either non-final, or the implementation of an interface that declares all public methods.
- All classes that do not extend or implement some specialized classes and interfaces required by the EJB framework.
```java
public class Employee {
   private int id;
   private String firstName; 
   private String lastName;   
   private int salary;  

   public Employee() {}
   public Employee(String fname, String lname, int salary) {
      this.firstName = fname;
      this.lastName = lname;
      this.salary = salary;
   }
   public int getId() {
      return id;
   }
   public void setId( int id ) {
      this.id = id;
   }
   public String getFirstName() {
      return firstName;
   }
   public void setFirstName( String first_name ) {
      this.firstName = first_name;
   }
   public String getLastName() {
      return lastName;
   }
   public void setLastName( String last_name ) {
      this.lastName = last_name;
   }
   public int getSalary() {
      return salary;
   }
   public void setSalary( int salary ) {
      this.salary = salary;
   }
}
```

#### Mapping
An Object/relational mappings are usually defined in an XML document. This mapping file instructs Hibernate how to map the defined class or classes to the database tables. Though many Hibernate users choose to write the XML by hand, a number of tools exist to generate the mapping document. These include XDoclet, Middlegen and AndroMDA for advanced Hibernate users. You should save the mapping document in a file with the format *<classname>.hbm.xml*. Sample mapping:
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
 "-//Hibernate/Hibernate Mapping DTD//EN"
 "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd"> 

<hibernate-mapping>
   <class name="Employee" table="EMPLOYEE">
      <meta attribute="class-description">
         This class contains the employee detail. 
      </meta>
      <id name="id" type="int" column="id">
         <generator class="native"/>
      </id>
      <property name="firstName" column="first_name" type="string"/>
      <property name="lastName" column="last_name" type="string"/>
      <property name="salary" column="salary" type="int"/>
   </class>
</hibernate-mapping>
```
When you prepare a Hibernate mapping document, we have seen that you map Java data types into RDBMS data types. The types declared and used in the mapping files are not Java data types; they are not SQL database types either. These types are called Hibernate mapping types, which can translate from Java to SQL data types and vice versa.

**Primitive types**

| Mapping type |	Java type |	ANSI SQL Type |
| --- | --- | --- |
| integer |	int or java.lang.Integer | INTEGER |
| long |	long or java.lang.Long |	BIGINT |
| short |	short or java.lang.Short |	SMALLINT|
| float |	float or java.lang.Float |	FLOAT|
| double |	double or java.lang.Double |	DOUBLE|
| big_decimal |	java.math.BigDecimal |	NUMERIC|
| character |	java.lang.String |	CHAR(1)|
| string |	java.lang.String |	VARCHAR|
| byte |	byte or java.lang.Byte |	TINYINT|
| boolean |	boolean or java.lang.Boolean |	BIT|
| yes/no |	boolean or java.lang.Boolean |	CHAR(1) ('Y' or 'N')|
| true/false |	boolean or java.lang.Boolean |	CHAR(1) ('T' or 'F')|

**Date and time types**

|Mapping type|	Java type|	ANSI SQL Type|
| --- | --- | --- |
|date|	java.util.Date or java.sql.Date	|DATE|
|time	|java.util.Date or java.sql.Time|	TIME|
|timestamp|	java.util.Date or java.sql.Timestamp	|TIMESTAMP|
|calendar	|java.util.Calendar	|TIMESTAMP|
|calendar_date	|java.util.Calendar	|DATE|

**Binary and large object types**

|Mapping type|	Java type|	ANSI SQL Type|
| --- | --- | --- |
|binary|	byte[]	|VARBINARY (or BLOB)|
|text	|java.lang.String|	CLOB|
|serializable|	any Java class that implements java.io.Serializable|	VARBINARY (or BLOB)|
|clob	|java.sql.Clob	|CLOB|
|blob	|java.sql.Blob	|BLOB|

**JDK-related types**

|Mapping type	|Java type	|ANSI SQL Type|
| --- | --- | --- |
|class|	java.lang.Class|VARCHAR|
|locale	|java.util.Locale	|VARCHAR|
|timezone	|java.util.TimeZone	|VARCHAR|
|currency|	java.util.Currency|	VARCHAR|

#### Sample Application Class
```java
import java.util.List; 
import java.util.Date;
import java.util.Iterator; 
import org.hibernate.HibernateException; 
import org.hibernate.Session; 
import org.hibernate.Transaction;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class ManageEmployee {
   private static SessionFactory factory; 
   public static void main(String[] args) {
      try{
         factory = new Configuration().configure().buildSessionFactory();
      }catch (Throwable ex) { 
         System.err.println("Failed to create sessionFactory object." + ex);
         throw new ExceptionInInitializerError(ex); 
      }
      ManageEmployee ME = new ManageEmployee();

      /* Add few employee records in database */
      Integer empID1 = ME.addEmployee("Zara", "Ali", 1000);
      Integer empID2 = ME.addEmployee("Daisy", "Das", 5000);
      Integer empID3 = ME.addEmployee("John", "Paul", 10000);

      /* List down all the employees */
      ME.listEmployees();

      /* Update employee's records */
      ME.updateEmployee(empID1, 5000);

      /* Delete an employee from the database */
      ME.deleteEmployee(empID2);

      /* List down new list of the employees */
      ME.listEmployees();
   }
   /* Method to CREATE an employee in the database */
   public Integer addEmployee(String fname, String lname, int salary){
      Session session = factory.openSession();
      Transaction tx = null;
      Integer employeeID = null;
      try{
         tx = session.beginTransaction();
         Employee employee = new Employee(fname, lname, salary);
         employeeID = (Integer) session.save(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
      return employeeID;
   }
   /* Method to  READ all the employees */
   public void listEmployees( ){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         List employees = session.createQuery("FROM Employee").list(); 
         for (Iterator iterator = 
                           employees.iterator(); iterator.hasNext();){
            Employee employee = (Employee) iterator.next(); 
            System.out.print("First Name: " + employee.getFirstName()); 
            System.out.print("  Last Name: " + employee.getLastName()); 
            System.out.println("  Salary: " + employee.getSalary()); 
         }
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
   /* Method to UPDATE salary for an employee */
   public void updateEmployee(Integer EmployeeID, int salary ){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         Employee employee = 
                    (Employee)session.get(Employee.class, EmployeeID); 
         employee.setSalary( salary );
		 session.update(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
   /* Method to DELETE an employee from the records */
   public void deleteEmployee(Integer EmployeeID){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         Employee employee = 
                   (Employee)session.get(Employee.class, EmployeeID); 
         session.delete(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
}
```






#### FAQ

**What is ORM?**

ORM stands for object/relational mapping. ORM is the automated persistence of objects in a Java application to the tables in a relational database.

**What does ORM consists of?**

An ORM solution consists of the followig four pieces:
- API for performing basic CRUD operations
- API to express queries refering to classes
- Facilities to specify metadata
- Optimization facilities: dirty checking, lazy associations fetching

**What are the ORM levels?**

The ORM levels are:
- Pure relational (stored procedure)
- Light objects mapping (JDBC)
- Medium object mapping
- Full object Mapping (composition, inheritance, polymorphism, persistence by reachability)

**What is Hibernate?**

Hibernate is a pure Java object-relational mapping (ORM) and persistence framework that allows you to map plain old Java objects to relational database tables using (XML) configuration files. Its purpose is to relieve the developer from a significant amount of relational data persistence-related programming tasks.

**Why do you need ORM tools like hibernate?**

The main advantage of ORM like hibernate is that it shields developers from messy SQL.

**What Does Hibernate Simplify?**

- Saving and retrieving your domain objects
- Making database column and table name changes
- Centralizing pre save and post retrieve logic
- Complex joins for retrieving related items
- Schema creation from object model

**What is the need for Hibernate xml mapping file?**

Hibernate mapping file tells Hibernate which tables and columns to use to load and store objects.

**What are the Core interfaces are of Hibernate framework?**
 
The five core interfaces are used in just about every Hibernate application. Using these interfaces, you can store and retrieve persistent objects and control transactions.
- Session interface
- SessionFactory interface
- Configuration interface
- Transaction interface
- Query and Criteria interfaces

**What role does the Session interface play in Hibernate?**

The Session interface is the primary interface used by Hibernate applications. It is a single-threaded, short-lived object representing a conversation between the application and the persistent store. It allows you to create query objects to retrieve persistent objects. `Session session = sessionFactory.openSession();`

Session interface role:
- Wraps a JDBC connection
- Factory for Transaction
- Holds a mandatory (first-level) cache of persistent objects, used when navigating the object graph or looking up objects by identifier

**What role does the SessionFactory interface play in Hibernate?**

The application obtains Session instances from a SessionFactory. There is typically a single SessionFactory for the whole applicationå¹¼reated during application initialization. The SessionFactory caches generate SQL statements and other mapping metadata that Hibernate uses at runtime. It also holds cached data that has been read in one unit of work and may be reused in a future unit of work `SessionFactory sessionFactory = configuration.buildSessionFactory();`

**What is the general flow of Hibernate communication with RDBMS?**

The general flow of Hibernate communication with RDBMS is:
- Load the Hibernate configuration file and create configuration object. It will automatically load all hbm mapping files
- Create session factory from configuration object
- Get one session from this session factory
- Create HQL Query
- Execute query to get list containing Java objects

**What is Hibernate Query Language (HQL)?**

Hibernate offers a query language that embodies a very powerful and flexible mechanism to query, store, update, and retrieve objects from a database. This language, the Hibernate query Language (HQL), is an object-oriented extension to SQL.

**How do you map Java Objects with Database tables?**
- First we need to write Java domain objects (beans with setter and getter).
- Write hbm.xml, where we map java class to table and database columns to Java class variables.

*SOURCE:* [developersbook.com](http://www.developersbook.com/hibernate/interview-questions/hibernate-interview-questions-faqs.php)
