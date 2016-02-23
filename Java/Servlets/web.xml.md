## WEB.XML File
The web.xml file is where your web app is configured. Here’s the basic structure of the web.xml file we started out with:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?> 
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
   version="3.0">
  <display-name>Welcome to Tomcat</display-name>
  <description>
     Welcome to My Java112 Site
  </description> 
<!-- Context Parameters ************************************************** -->
<!-- Servlet and JSP Configurations ************************************** -->
<!-- Servlet Mappings **************************************************** -->
<!-- Home Page *********************************************************** -->
  <welcome-file-list>
    <welcome-file>/WEB-INF/index.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```
#### Configuring Servlets (The old way)
When you add a JSP page or a Servlet to your web app, you need to both declare them and map them.
All the declarations have to be together and all the mappings have to be together. You can’t intermingle them!
This is how the configuration file was used before:
```xml
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
   version="2.5"> 
<?xml version="1.0" encoding="ISO-8859-1"?>
  <display-name>Welcome to My Shiny App</display-name>
  <description>
     Welcome to My Shiny App.
  </description> 
<!-- Servlet and JSP Declarations -->
  <!-- A JSP page -->
  <servlet>
    <servlet-name>Declarations</servlet-name>
    <jsp-file>/declarations.jsp</jsp-file>
  </servlet> 
  <!-- A Servlet -->
  <servlet>
    <servlet-name>TrivialServlet</servlet-name>
    <servlet-class>java112.project2.TrivialServlet</servlet-class>
  </servlet>   
<!-- Servlet and JSP Mappings --> 
  <!-- A Mapping for a JSP page -->
  <servlet-mapping>
    <servlet-name>Declarations</servlet-name>
    <url-pattern>/declarations</url-pattern>
  </servlet-mapping>  
  <!-- A Mapping for a Servlet -->
  <servlet-mapping>
    <servlet-name>TrivialServlet</servlet-name>
    <url-pattern>/trivial</url-pattern>
  </servlet-mapping>
</web-app>
```
**Process:**

To add a new JSP page to your web app you need to do these steps:
- Create your .jsp file and place it in your public_html/ directory.
- Open the web.xml file from your config directory.
- In the Servlet and JSP Declarations section of the web.xml file, add an element:
```xml
<servlet>
 <servlet-name>Declarations</servlet-name>
 <jsp-file>/declarations.jsp</jsp-file>
</servlet>
```
The `<servlet-name>` can be anything you want without spaces. It will have to be unique from all the other declarations. The `<jsf-file>` is the name of the jsp file. You will have to all the “/” to the front of the name. If you have your jsp files in another directory inside of public_html, then you need to add: /jsp/declarations.jsp.
- Add a mapping element to the Servlet and JSP Mappings section of the web.xml file. The `<servlet-name>` must match the declaration element that you are mapping to. The `<url-pattern>` element can be anything you want without spaces. You can even map to a different extension, like .html or .asp. I recommend not using an extension and making a nice simple, pretty URL. You should not use an extension of .jsp!

#### To add a new servlet to your web app:

- Create your packaged servlet class and place it in the correct directory for that package.
- In the Servlet and JSP Declarations section of the web.xml file, add an element:
```xml
<servlet>
 <servlet-name>TrivialServlet</servlet-name>
 <servlet-class>java112.project2.TrivialServlet</servlet-class>
</servlet>
```
The <servlet-name> can be anything you want without spaces. It will have to be unique from all the other declarations. The <servlet-class> element will be the full package name of your class.
- Add a mapping element to the Servlet and JSP Mappings section of the web.xml file:
```xml
<servlet-mapping>
 <servlet-name>TrivialServlet</servlet-name>
 <url-pattern>/trivial</url-pattern>
</servlet-mapping>
```
The `<servlet-name>` element must match the declaration that you are mapping to. The `<url-pattern>` element can be anything you want without spaces. You can even map to a different extension, like .html or .asp. I recommend not using an extension and making a nice simple, pretty URL. You should also not use the word “servlet” in this URL.

#### Accessing Mapped Pages and Servlets:
In your web app, you will always use the mapped URL when accessing your pages and servlets.
<li><a href="/app/declarations">JSP Declarations</a></li>
You need to have the name of your web app in front of the mapped URL. In this case that’s “/app/”.
