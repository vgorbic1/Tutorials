## Order of Servlet Loadings
The element `load-on-startup` indicates that this servlet should be loaded (instantiated and have its init() called) on the startup 
of the Web application. The element content of this element must be an integer indicating the order in which the servlet should be 
loaded. If the value is a negative integer, or the element is not present, the container is free to load the servlet whenever it 
chooses. If the value is a positive integer or 0, the container must load and initialize the servlet as the application is deployed. 
The container must guarantee that servlets marked with lower integers are loaded before servlets marked with higher integers. 
The container may choose the order of loading of servlets with the same load-on-startup value.

In short value >= 0 means that the servlet is loaded when the web-app is deployed or when the server starts. value < 0 : servlet is loaded whenever the container feels like.
```xml
<servlet>
    <servlet-name>AxisServlet</servlet-name>
    <display-name>Apache-Axis Servlet</display-name>
    <servlet-class>com.foo.framework.axis2.http.FrameworkServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet> 
```
Using annotations:
```java
@WebServlet(
    name = "ApplicationStartup",
    urlPatterns = { "/startup" },
    loadOnStartup = 1
)
```
