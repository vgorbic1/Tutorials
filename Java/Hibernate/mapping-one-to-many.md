## Hibernate One-to-Many XML Mapping Example
Create a sample Hibernate-based application to manage the following entity relationship:

![hibernate-one-to-many-diagram](https://cloud.githubusercontent.com/assets/13823751/13234128/ca5ac55a-d97c-11e5-8454-29682ad62b5f.png)

In this relationship, a category can contain one or many products.

#### Creating sample database and tables
```sql
create database stockdb;
use stockdb;
 
CREATE TABLE `category` (
  `category_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  PRIMARY KEY (`category_id`)
);
 
CREATE TABLE `product` (
  `product_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `description` varchar(512) NOT NULL,
  `price` float NOT NULL,
  `category_id` int(11) NOT NULL,
  PRIMARY KEY (`product_id`),
  KEY `fk_category` (`category_id`),
  CONSTRAINT `fk_category` FOREIGN KEY (`category_id`) REFERENCES `category` (`category_id`)
);
```
#### Coding Hibernate Model Classes
Category.java file:
```java
package net.codejava.hibernate;
 
import java.util.Set;
 
public class Category {
 
    private long id;
    private String name;
 
    private Set<Product> products;
 
    public Category() {
    }
 
    public Category(String name) {
        this.name = name;
    }
 
    // getters and setters...
 
}
```
Product.java file:
```java
package net.codejava.hibernate;
 
public class Product {
    private long id;
    private String name;
    private String description;
    private float price;
    private Category category;
 
    public Product() {
    }
 
    public Product(String name, String description, float price,
            Category category) {
        this.name = name;
        this.description = description;
        this.price = price;
        this.category = category;
    }
 
 
    // getters and setters...
 
}
```
A Category contains a set of Products: `private Set<Product> products;` and a Product links back to its category: `private Category category;`
#### Creating Hibernate Mapping Files
Create two XML files `Category.hbm.xml` and `Product.hbm.xml` to tell Hibernate how to map the JavaBean classes above with the database tables.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping package="net.codejava.hibernate">
    <class name="Category" table="CATEGORY">
        <id name="id" column="CATEGORY_ID">
            <generator class="native"/>
        </id>
        <property name="name" column="NAME" />
 
        <set name="products" inverse="true" cascade="all">
            <key column="CATEGORY_ID" not-null="true" />
            <one-to-many class="Product"/>
        </set>
    </class> 
</hibernate-mapping>
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping package="net.codejava.hibernate">
    <class name="Product" table="PRODUCT">
        <id name="id" column="PRODUCT_ID">
            <generator class="native"/>
        </id>
        <property name="name" column="NAME" />
        <property name="description" column="DESCRIPTION" />
        <property name="price" column="PRICE" type="float" />
         
        <many-to-one name="category" class="Category"
            column="CATEGORY_ID" not-null="true"/>
    </class> 
</hibernate-mapping>
```
Pay attention to the attribute `inverse=”true”` of the `<set>` element in the `Category.hbm.xml file`. That means this side (Category) is not the relationship owner. Instead, it is the reverse side (Product) is the relationship owner. Because the product table has a foreign key that refers to the category table, it is the owner of this one-to-many relationship. So keep in mind that using `inverse=”true”` is mandatory in this case.

#### Writing Hibernate Configuration File
Create the Hibernate configuration file `hibernate.cfg.xml` to specify database type, connection details and the mapping files:
```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>       
  <session-factory>
    <!-- Database connection settings -->
    <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
    <property name="connection.url">jdbc:mysql://localhost:3306/stockdb</property>
    <property name="connection.username">root</property>
    <property name="connection.password">secret</property>
    <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
    <property name="show_sql">true</property>
     
    <mapping resource="net/codejava/hibernate/Category.hbm.xml"/>
    <mapping resource="net/codejava/hibernate/Product.hbm.xml"/>
       
  </session-factory>
</hibernate-configuration>
```
Update the database username and password corresponding to your database settings.
#### Coding a Test Program
```java
package net.codejava.hibernate;
 
import java.util.HashSet;
import java.util.Set;
 
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;
import org.hibernate.service.ServiceRegistry;
import org.hibernate.service.ServiceRegistryBuilder;
 
/**
 *
 * This program demonstrates using Hibernate framework to manage a
 * bidirectional one-to-many association.
 * @author www.codejava.net
 *
 */
public class StockManager {
 
    public static void main(String[] args) {
        // loads configuration and mappings
        Configuration configuration = new Configuration().configure();
        ServiceRegistryBuilder registry = new ServiceRegistryBuilder();
        registry.applySettings(configuration.getProperties());
        ServiceRegistry serviceRegistry = registry.buildServiceRegistry();
         
        // builds a session factory from the service registry
        SessionFactory sessionFactory = configuration.buildSessionFactory(serviceRegistry);
         
        // obtains the session
        Session session = sessionFactory.openSession();
        session.beginTransaction();
         
        Category category = new Category("Computer");
         
        Product pc = new Product("DELL PC", "Quad-core PC", 1200, category);
         
        Product laptop = new Product("MacBook", "Apple High-end laptop", 2100, category);
         
        Product phone = new Product("iPhone 5", "Apple Best-selling smartphone", 499, category);
         
        Product tablet = new Product("iPad 3", "Apple Best-selling tablet", 1099, category);
         
        Set<Product> products = new HashSet<Product>();
        products.add(pc);
        products.add(laptop);
        products.add(phone);
        products.add(tablet);
         
        category.setProducts(products);
         
        session.save(category);
         
        session.getTransaction().commit();
        session.close();       
    }
}
```
Output of the program:
```
Hibernate: insert into CATEGORY (NAME) values (?)
Hibernate: insert into PRODUCT (NAME, DESCRIPTION, PRICE, CATEGORY_ID) values (?, ?, ?, ?)
Hibernate: insert into PRODUCT (NAME, DESCRIPTION, PRICE, CATEGORY_ID) values (?, ?, ?, ?)
Hibernate: insert into PRODUCT (NAME, DESCRIPTION, PRICE, CATEGORY_ID) values (?, ?, ?, ?)
Hibernate: insert into PRODUCT (NAME, DESCRIPTION, PRICE, CATEGORY_ID) values (?, ?, ?, ?)
```
[SOURCE](http://www.codejava.net/frameworks/hibernate/hibernate-one-to-many-xml-mapping-example)
