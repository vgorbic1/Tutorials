## XML Based Spring Configuration File
Spring supports XML-based configuration since version 1.0 as well as annotation-based configuration strting version 2.5.

The root element of a Spring configuration file is always beans:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:p="http://www.springframework.org/schema/p"
  xsi:schemaLocation="http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    ...
</beans>
```
You can add more shemas to the schemaLocation attribute if you need more Spring functionality in your application.

You can split your XML configuration file into multiple files or have a main XML conf file that imports others:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:p="http://www.springframework.org/schema/p"
  xsi:schemaLocation="http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    
  <import resource="config1.xml" />
  <import resource="module2/config2.xml" />
  <import resource="/resources/config3.xml" />
  
</beans>
```
#### Creating a Bean Instance with a Constructor
To get an instance of a bean, call the getBean method on the ApplicationContext. The following configuration file
contains the definition of a singel bean named **product**:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:p="http://www.springframework.org/schema/p"
  xsi:schemaLocation="http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    
  <bean name="product" class="app01a.bean.Product" />
  
</beans>
```
This bean declaration tells Spring to instantiate the Product class using its no-argument (default) constructor.
Spring throws an exception if such constructor does not exist or another constructor is defined without default constructor.
This no-argument constructor does not have to be public. You can use **name** or **id** to identify your bean.

To create an instance of **Product**, call the getBean method passing the bean name or id and its class:
```java
ApplicationContext context =
  new ClassPathXmlApplicationContext(
    new String[] {"spring-config.xml"});
Product product1 = context.getBean("product", Product.class);
prduct1.setName("Butter");
System.out.println("product1: " + product1.getName());
```
