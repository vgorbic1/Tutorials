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
