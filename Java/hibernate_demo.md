## Hibernate Demo

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
            jdbc:mysql://localhost:3306/sample
        </property>
        <property name="connection.driver_class">
            com.mysql.jdbc.Driver
        </property>
        <property name="connection.username">
            admin
        </property>
        <property name="connection.password">
            admin
        </property>
        <mapping resource="Employee.hbm.xml" />
        <mapping class="edu.madisoncollege.entjava.entity.Employee" />
    </session-factory>

</hibernate-configuration>
```
