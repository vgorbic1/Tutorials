## Hibernate Demo
This demonstrates Hibernate with MySQL database.

#### Step One
Add hibernate external libraries or plugin. Make sure you have geronimo.jar library plugged in.

#### Step Two
Create the Hibernate configuration XML file in resources directory and name it hibernate.cfh.xml:
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
Create a database and a table:
```
