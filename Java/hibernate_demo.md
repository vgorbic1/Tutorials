## Hibernate Demo
This demonstrates Hibernate with MySQL database.

#### Step One
Add hibernate external libraries or plugin. Make sure you have geronimo.jar library plugged in.

#### Step Two
Create the Hibernate configuration XML file in resources directory and name it *hibernate.cfh.xml*
```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <property name="dialect">
            org.hibernate.dialect.MySQL5Dialect
        </property>
        <property name="connection.url">
            jdbc:mysql://localhost:3306/sample /// change to your database configuration
        </property>
        <property name="connection.driver_class">
            com.mysql.jdbc.Driver
        </property>
        <property name="connection.username">admin</property>  /// change to your database username
        <property name="connection.password">admin</property>  /// change to your database password
        <mapping resource="Employee.hbm.xml" />   /// change to your entity (Class that represents MySQL table) file name
        <mapping class="my.package.name.entity.Employee" />  // change to the classpath within your package
    </session-factory>

</hibernate-configuration>
```

#### Step Three
Create a new database.
```
mysql> CREATE DATABASE sample;
```
Select the database you just created.
```
mysql> use sample
```
Create a user to access the database you just created. 
You can name this user whatever you like, and give it whatever 
password you like.
```
mysql> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';
```
Give the new user "crud" privileges on the database.
```
mysql> GRANT ALL PRIVILEGES ON sample.* TO 'admin'@'localhost';
```
Add a new table.
```sql
create table employees (
    emp_id          int(6) NOT NULL auto_increment,
    first_name      varchar(25),
    last_name       varchar(30),
    ssn             varchar(20),
    dept            varchar(10),
    room            varchar(10),
    phone           varchar(10),
    PRIMARY KEY  (emp_id)
);
```
Add some rows.
```sql
insert into employees values (101, 'Joe', 'Coyne', '111-22-3333', 'HR', '125', '555-3726');
insert into employees values (102, 'Fred', 'Hensen', '222-33-4444', 'Eng', '126', '555-3727');
insert into employees values (103, 'Ethyl', 'Roselle', '333-44-5555', 'Admin', '127', '555-3728');
insert into employees values (104, 'Barney', 'Curry', '444-55-6666', 'IT', '128', '555-3729');
```
#### Step Four
Create one javabean (Model) representing the data on one the table. *Employee.java*. As a normal javabean, the class should have private properties that represents columns of the table. The class should have an empty constructor as well as overloaded constructor with all properties as parameters. Also create setters and getters for each property. Create a 'toString()' method for debugging:
```java
package /your package path/ .entity;
public class Employee {

    private int employeeId;
    private String firstName;
    private String lastName;
    private String ssn;
    private String department;
    private String room;
    private String phone;

    public Employee() {
    }

    public Employee(int employeeId,
                    String firstName,
                    String lastName,
                    String ssn,
                    String department,
                    String room,
                    String phone) {
        this.employeeId = employeeId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.ssn = ssn;
        this.department = department;
        this.room = room;
        this.phone = phone;
    }

    public int getEmployeeId() {
        return employeeId;
    }

    public void setEmployeeId(int employeeId) {
        this.employeeId = employeeId;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getSsn() {
        return ssn;
    }

    public void setSsn(String ssn) {
        this.ssn = ssn;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public String getRoom() {
        return room;
    }

    public void setRoom(String room) {
        this.room = room;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "employeeId=" + employeeId +
                ", firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", ssn='" + ssn + '\'' +
                ", department='" + department + '\'' +
                ", room='" + room + '\'' +
                ", phone='" + phone + '\'' +
                '}';
    }
}
```
You may put the file into a subdirrectory of your project's packaged source files. Call the directory *entity*. This is a directory where all Model files will go.

Create another directory next to *entity* for DAO files and name it *persistence*. 

#### Step Five
Create a *Database.java* file and put it into *persistence*. This file provides database info and is needed for connection to the database.
```java
package /your package path/ .persistence;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import org.apache.log4j.*; // if you want to log errors. You need to plug in the log4j external library.

public class Database {
    private static Database instance = new Database();
    private Connection connection;
    private final Logger log = Logger.getLogger(this.getClass()); // Optional. use if you need to log errors.

    private Database() {
    }

    // create Database singleton
    public static Database getInstance() {
        return instance;
    }

    public Connection getConnection() {
        return connection;
    }

    public void connect() throws Exception {
        if (connection != null)
            return;

        // Following values should not be hard-coded in a real application.
        try {
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            throw new Exception("Error: MySQL driver not found");
        }
        String url = "jdbc:mysql://localhost:3306/sample"; //Update with your database connection info
        connection = DriverManager.getConnection(url, "admin", "admin"); //Update with your database connection info
    }

    public void disconnect() {
        if (connection != null) {
            try {
                connection.close();
            } catch (SQLException e) {
                log.error("Cannot close connection",e);
            }
        }
        connection = null;
    }
}
```

#### Step Six
Create a mapping file to map your model class to the database table. Name it *Employee.hbm.xml* and put to the resources directory.
```xml
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">

<hibernate-mapping>
    <class name="your.package.path.entity.Employee" table="employee"> /// Change the path to the entity
        <meta attribute="class-description">This class contains the employee detail.</meta>
        <!-- Map primary key (id) to the corresponding column -->
        <id name="employeeId" type="int"
            column="emp_id">
            <generator class="native"/>
        </id>
        <!--Add a property for all other instance variables/columns-->
        <property name="firstName" column="first_name" type="string"/>
        <property name="lastName" column="last_name" type="string"/>
        <property name="ssn" column="ssn" type="string"/>
        <property name="department" column="ssn" type="string"/>
        <property name="room" column="room" type="string"/>
        <property name="phone" column="phone" type="string"/>
    </class>
</hibernate-mapping>
```

#### Step Seven
Create interface for the 
