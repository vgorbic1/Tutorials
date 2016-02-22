## Hibernate One-to-Many Using Join Table XML Mapping Example
The following entity relationship diagram depicts the association:
![hibernate-many-to-many-diagram](https://cloud.githubusercontent.com/assets/13823751/13234547/ceb64e2e-d97e-11e5-8931-93c94f3995ed.png)
Here, a category can contain from one to many occurrences of article. The CategoryArticle is the join table between them.
#### Creating Database Tables
```sql
CREATE DATABASE `newsdb`;
 
use newsdb;
 
CREATE TABLE `category` (
  `category_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  PRIMARY KEY (`category_id`)
);
 
 
CREATE TABLE `article` (
  `article_id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(70) NOT NULL,
  `description` varchar(250) NOT NULL,
  `keywords` varchar(150) NOT NULL,
  `content` text NOT NULL,
  PRIMARY KEY (`article_id`)
);
 
 
CREATE TABLE `categoryarticle` (
  `category_id` int(11) NOT NULL,
  `article_id` int(11) NOT NULL,
  PRIMARY KEY (`category_id`,`article_id`),
  KEY `fk_category` (`category_id`),
  KEY `fk_article` (`article_id`),
  CONSTRAINT `fk_article` FOREIGN KEY (`article_id`) REFERENCES `article` (`article_id`),
  CONSTRAINT `fk_category` FOREIGN KEY (`category_id`) REFERENCES `category` (`category_id`)
);
```
#### Coding Hibernate Model Classes
Create two Java files `Category.java` and `Article.java` corresponding to the tables category and article:
```java
package net.codejava.hibernate;
 
import java.util.Set;
 
public class Category {
 
    private long id;
    private String name;
 
    private Set<Article> articles;
 
    public Category() {
    }
 
    public Category(String name) {
        this.name = name;
    }
 
    // getters and setters...
}
```
```java
package net.codejava.hibernate;
 
public class Article {
    private long id;
    private String title;
    private String description;
    private String keywords;
    private String content;
 
    private Category category;
 
    public Article() {
    }
 
    public Article(String title, String description, String keywords,
            String content, Category category) {
        this.title = title;
        this.description = description;
        this.keywords = keywords;
        this.content = content;
        this.category = category;
    }
 
    // getters and setters...
}
```
The Category class has a set of articles and the Article class has a reference to its category. This is a typical configuration for a bidirectional one-to-many association. And note that we don’t have to write model class for the join table.
#### Writing Hibernate Mapping Files
Create two Hibernate mapping files `Category.hbm.xml` and `Article.hbm.xml`:
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
 
        <set name="articles" table="CategoryArticle" cascade="all">
            <key column="CATEGORY_ID" not-null="true" />
            <many-to-many column="ARTICLE_ID" class="Article" unique="true"/>
        </set>
    </class> 
</hibernate-mapping>
```
```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping package="net.codejava.hibernate">
    <class name="Article" table="ARTICLE">
        <id name="id" column="ARTICLE_ID">
            <generator class="native"/>
        </id>
        <property name="title" column="TITLE" />
        <property name="description" column="DESCRIPTION" />
        <property name="keywords" column="KEYWORDS" />
        <property name="content" column="CONTENT" />
 
        <join table="CategoryArticle" inverse="true">
            <key column="ARTICLE_ID"/>
            <many-to-one name="category" column="CATEGORY_ID" not-null="true"/>
        </join>
    </class> 
</hibernate-mapping>
```
- We specify the join table `CategoryArticle` for both sides, in the `<set>` element of the `Category.hbm.xml` file and in the `<join>` element of the` Article.hbm.xml` file.
- `Category.hbm.xml`: The attribute `cascade=”all”` tells Hibernate to update changes to the children (article) automatically when the parent (category) has changed.
- `Article.hbm.xml`: The attribute `inverse=”true”` tells Hibernate that the relationship owner is on the reverse side (the join table). Specifying this attribute is required for a one-to-many association.

#### Writing Hibernate Configuration File
Write code for the Hibernate configuration file `hibernate.cfg.xml`.
```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>       
  <session-factory>
    <!-- Database connection settings -->
    <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
    <property name="connection.url">jdbc:mysql://localhost:3306/newsdb</property>
    <property name="connection.username">root</property>
    <property name="connection.password">secret</property>
    <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
    <property name="show_sql">true</property>
     
    <mapping resource="net/codejava/hibernate/Category.hbm.xml"/>
    <mapping resource="net/codejava/hibernate/Article.hbm.xml"/>
       
  </session-factory>
</hibernate-configuration>
```
You may need to change the username and password according to your MySQL account.
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
 * This program demonstrates how to use Hibernate framework to manage
 * a one-to-many association on a join table.
 * @author www.codejava.net
 *
 */
public class ArticlesManager {
 
    public static void main(String[] args) {
        // loads configuration and mappings
        Configuration configuration = new Configuration().configure();
        ServiceRegistryBuilder registry = new ServiceRegistryBuilder();
        registry.applySettings(configuration.getProperties());
        ServiceRegistry serviceRegistry = registry.buildServiceRegistry();
 
        // builds a session factory from the service registry
        SessionFactory sessionFactory = configuration
                .buildSessionFactory(serviceRegistry);
 
        // obtains the session
        Session session = sessionFactory.openSession();
        session.beginTransaction();
 
        Category category = new Category("Hibernate Framework");
 
        Article articleOne = new Article("One-to-One Mapping",
                "One-to-One XML Mapping Tutorial", "Hibernate,One-to-One",
                "Content of One-to-One XML Mapping Tutorial", category);
        Article articleTwo = new Article("One-to-Many Mapping",
                "One-to-Many XML Mapping Tutorial", "Hibernate,One-to-Many",
                "Content of One-to-Many XML Mapping Tutorial", category);
        Article articleThree = new Article("Many-to-Many Mapping",
                "Many-to-Many XML Mapping Tutorial", "Hibernate,Many-to-Many",
                "Content of Many-to-Many XML Mapping Tutorial", category);
 
        Set<Article> articles = new HashSet<Article>();
        articles.add(articleOne);
        articles.add(articleTwo);
        articles.add(articleThree);
 
        category.setArticles(articles);
 
        session.save(category);
 
        session.getTransaction().commit();
        session.close();
    }
 
}
```
Output of the program:
```
Hibernate: insert into CATEGORY (NAME) values (?)
Hibernate: insert into ARTICLE (TITLE, DESCRIPTION, KEYWORDS, CONTENT) values (?, ?, ?, ?)
Hibernate: insert into ARTICLE (TITLE, DESCRIPTION, KEYWORDS, CONTENT) values (?, ?, ?, ?)
Hibernate: insert into ARTICLE (TITLE, DESCRIPTION, KEYWORDS, CONTENT) values (?, ?, ?, ?)
Hibernate: insert into CategoryArticle (CATEGORY_ID, ARTICLE_ID) values (?, ?)
Hibernate: insert into CategoryArticle (CATEGORY_ID, ARTICLE_ID) values (?, ?)
Hibernate: insert into CategoryArticle (CATEGORY_ID, ARTICLE_ID) values (?, ?)
```
