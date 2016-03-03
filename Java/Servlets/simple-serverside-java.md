## Execute Serverside Java

* Install Tomcat
* Create a Java Servlet and name it something. Say `HelloWorld.java`.
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

// Extend HttpServlet class
public class HelloWorld extends HttpServlet {
    private String message;

    public void init() throws ServletException {
        // Do required initialization
        message = "Hello World";
    }

    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Set response content type
        response.setContentType("text/html");
        // Actual logic goes here.
        PrintWriter out = response.getWriter();
        out.println("<h1>" + message + "</h1>");
    }

    public void destroy() {
        // do nothing.
    }
}
```
* Using Command Prompt navigate to the folder with the file.
* Compile the file. Include the classpath to the Servlet jars, that could be found in the Tomcat installation.
```
> javac -cp /path-to/lib/servlet-api.jar HelloWorld.java 
```
* Deploy it to Tomcat. Inside webapps directory of Tomcat create a directory for the new application. Call the new app say `hello` This directory should also have `WEB-INF` subdirectory, which will contain another subfolder called `classes` and a deployment descriptor file `web.xml`. Put your compiled `HelloWorld.class` file into the `classes` directory. Create the `web.xml` file:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
  version="3.0"
  metadata-complete="true">

  <display-name>Hello World Java Application</display-name>
  <description>
    A simple java app
  </description>

  <servlet>
    <servlet-name>hw</servlet-name>
    <servlet-class>HelloWorld</servlet-class>
  </servlet>
 
  <servlet-mapping>
    <servlet-name>hw</servlet-name>
    <url-pattern>/helloWorld</url-pattern>
  </servlet-mapping>

</web-app>
```
* Check whether the app is working at your browser:
```
localhost:8080/hello/helloWorld
```
If something goes wrong check Tomcat log files.
