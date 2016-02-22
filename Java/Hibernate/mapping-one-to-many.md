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
