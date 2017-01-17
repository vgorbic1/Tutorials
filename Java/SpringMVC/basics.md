## SpringMVC basics
#### Add Tomcat plugin to your Maven project
Add Tomcat7 plugin to your project's pom.xml file right below dependencies:
```java
<build>
  <pluginManagement>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.2</version>
        <configuration>
          <verbose>true</verbose>
          <source>1.8</source>
          <target>1.8</target>
          <showWarnings>true</showWarnings>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
          <path>/</path>
          <contextReloadable>true</contextReloadable>
        </configuration>
      </plugin>
    </plugins>
  </pluginManagement>
</build>
```

#### Add SpringMVC to your Maven project
Add SpringMVC library to your project's pom.xml:
```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
  <version>4.2.2.RELEASE</version>
</dependency>
```
Maven will add all SpringMVC jars you need.

#### Add Front Controller (Dispatcher servlet) to your project
Add the following to your deployment descriptor (web.xml)
```xml
<servlet>
  <servlet-name>dispatcher</servlet-name>
  <servlet-class>
    org.springframework.web.servlet.DispatcherServlet
  </servlet-class>
  <init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/do-servlet.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
<servlet-name>dispatcher</servlet-name>
<url-pattern>/spring-mvc/*</url-pattern>
</servlet-mapping>
```

#### Add SpringMVC configuration (component scan) file:
Add a file to WEB-INF folder and call it "do-servlet.xml" as you defined above in web.xml.
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:context="http://www.springframework.org/schema/context"
  xmlns:mvc="http://www.springframework.org/schema/mvc"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
  http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
  http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
    <context:component-scan base-package="com.in28minutes" />
    <mvc:annotation-driven />
</beans>
```

#### Add Simple Controller (Handler)
This controller will handle a particular url (/login) request and send a string back to the browser:
```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
@Controller
public class LoginController {
  @RequestMapping(value = "/login")
  @ResponseBody
  public String showUsername() {
    return "username";
  }
}
```
