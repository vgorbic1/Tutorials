## Java Web Application

A web app is just a directory, but the directory has to be structured just right. Here are some of the elements that are required:
•	A WEB-INF/ directory.
•	A classes/ in the WEB-INF directory.
•	A web.xml file in the WEB-INF directory.
•	A META-INF/ directory.
•	A MANIFEST.MF file in the META-INF directory.
•	All the static files for your site.
•	A lib/ directory to contain jar files your app needs.
Then the entire directory is zipped into a file and named filname.war. Then we have to move the file to your tomcat/webapps/ directory.

When you add a JSP page or a Servlet to your web app, you need to both declare them and map them.
The web.xml file is where your web app is configured.
The old way to configure servlet was to modify web.xml file. All the declarations have to be together and all the mappings have to be together. You can’t intermingle them:
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
The modern way to configure servlet right in the servlet file:
@WebServlet(name = "trivialServlet", 
            urlPatterns = { "/trivial", "/simple" })

Adding New Jsp Page
To add a new JSP page to your web app you need to do these steps:
1. Create your .jsp file and place it in your public_html/ directory.
2. Open the web.xml file from your config directory.
In the Servlet and JSP Declarations section of the web.xml file, add an element like this.
<servlet>
 <servlet-name>Declarations</servlet-name>
 <jsp-file>/declarations.jsp</jsp-file>
</servlet>
The <servlet-name> can be anything you want without spaces. It will have to be unique from all the other declarations.
The <jsf-file> is the name of the jsp file. You will have to add the “/” to the front of the name. If you have your jsp files in another directory inside of public_html, then you need to add: /jsp/declarations.jsp.
3. Add a mapping element to the Servlet and JSP Mappings section of the web.xml file.
The <servlet-name> must match the declaration element that you are mapping to. The <url-pattern> element can be anything you want without spaces. You can even map to a different extension, like .html or .asp, but do not use an extension of .jsp!

Adding A New Servlet
To add a new servlet to your web app you need to follow these steps:
1. Create your packaged servlet class and place it in the correct directory for that package.
In the Servlet and JSP Declarations section of the web.xml file, add an element like this.
<servlet>
 <servlet-name>TrivialServlet</servlet-name>
 <servlet-class>java112.project2.TrivialServlet</servlet-class>
</servlet>
The <servlet-name> can be anything you want without spaces. It will have to be unique from all the other declarations.
The <servlet-class> element will be the full package name of your class.
2.  Add a mapping element to the Servlet and JSP Mappings section of the web.xml file.
<servlet-mapping>
 <servlet-name>TrivialServlet</servlet-name>
 <url-pattern>/trivial</url-pattern>
</servlet-mapping>
The <servlet-name> element must match the declaration that you are mapping to. The <url-pattern> element can be anything you want without spaces. You can even map to a different extension, like .html or .asp. You should also not use the word “servlet” in this URL.

Accessing Mapped Pages And Servlets
Use the mapped URL when accessing your pages and servlets in your app:
<li><a href="/java112/declarations">JSP Declarations</a></li>
You need to have the name of your web app in front of the mapped URL. In this case that’s “/java112/”.
