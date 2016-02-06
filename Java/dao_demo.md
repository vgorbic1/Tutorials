## DAO demo with MySQL

####Step One
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
#### Step Two
Create one javabean (Model) representing the data on one the table. *Employee.java*. As a normal javabean, the class should have private properties that represents columns of the table. The class should have an empty constructor as well as overloaded constructor with all properties as parameters. Also create setters and getters for each property. Create a 'toString()' method for debugging:
```java
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

#### Step Three
Create a *Database.java* file and put it into *persistence*. This file provides database info and is needed for connection to the database.
```java
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
#### Step Four
Create a DAO interface file. Name it *EmployeeDao.java*. Put it to *persistence* directory.
```java
import ... .entity.Employee;  // Import Employee class from entity subdirectory
import java.util.List;  // Import list to represent all rows of the table

public interface EmployeeDao {
    public List<Employee> getAllEmployees();  // Manifest a method to display all employees (all rows of the table)
    public void updateEmployee(Employee employee);  // Manifest a method to rewrite (insert) an employee
    public void deleteEmployee(Employee employee);  // Manifest a method to remove an employee
    public int addEmployee(Employee employee); // Manifest a method to add new emploee
}
```

#### Step Five
Create an implementation of the *EmploeeDao.java* interface. Name the file *EmployeeDaoWithSQL.java. Put the file into *persistence* directory.
```java
package ... .persistence; // Import persistence subdirectory
import ... .entity.Employee; // Import Employee class from entity subdirectory
import org.apache.log4j.Logger; // Optionally import a logger
import java.sql.Connection; // We need this stuff to connect to database
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList; 
import java.util.List;

public class EmployeeDaoWithSQL implements EmployeeDao {
    private final Logger log = Logger.getLogger(this.getClass());  // Optionally engage a logger

    @Override
    public List<Employee> getAllEmployees() {
        List<Employee> employees = new ArrayList<>();
        Database database = Database.getInstance();
        Connection connection = null;
        String sql = "select * from employees order by emp_id";

        try {
            database.connect();
            connection = database.getConnection();
            Statement selectStatement = connection.createStatement();
            ResultSet results = selectStatement.executeQuery(sql);
            while (results.next()) {
                Employee employee = createEmployeeFromResults(results); // iterate over the resultset, adding each user to the list
                employees.add(employee);
            }
            database.disconnect();
        } catch (SQLException e) {
            log.error("SQL Exception: ", e);
        } catch (Exception e) {
            log.error(e);
        }
        return employees;
    }

    @Override
    public void updateEmployee(Employee employee) {

    }

    @Override
    public void deleteEmployee(Employee employee) {

    }

    @Override
    public int addEmployee(Employee employee) {
        return 0;
    }

    private Employee createEmployeeFromResults(ResultSet results) throws SQLException {  // Map the table column to object properties
        Employee employee = new Employee();
        employee.setEmployeeId(results.getInt("emp_id"));
        employee.setFirstName(results.getString("first_name"));
        employee.setLastName(results.getString("last_name"));
        employee.setSsn(results.getString("ssn"));
        employee.setDepartment(results.getString("room"));
        employee.setPhone(results.getString("phone"));
        return employee;
    }
}
```
#### Step Six
Write tests for *EmployeeDaoWithSQL* class methods to test database functionality. They are automated with Intellij IDEA if you preinstall jUnit external library.
