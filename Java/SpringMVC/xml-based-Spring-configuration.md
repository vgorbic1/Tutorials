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
