## Security Declarative. Demo
#### The Home Page
```html
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<html>
<head>
<title>hot-dot-com.com!</title>
<link rel=stylesheet
href="company-styles.css"
type="text/css">
</head>
<body>
<table border=5 align="center">
<tr><th class="title">hot-dot-com.com!</table>
<p>
<h3>welcome to the ultimate dot-com company!</h3>
please select one of the following:
<ul>
<li><a href="investing/">investing</a>.
guaranteed growth for your hard-earned dollars!
<li><a href="business/">business model</a>.
new economy strategy!
<li><a href="history/">history</a>.
fascinating company history.
</ul>
</body>
```
#### The Deployment Descriptor (web.xml)
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE web-app PUBLIC
"-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
"http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
<web-app>

  <!-- Give name to FinalizePurchaseServlet. This servlet
  will later be mapped to the URL /ssl/FinalizePurchase
  (by means of servlet-mapping and url-pattern).
  Then, that URL will be designated as one requiring
  SSL (by means of security-constraint and
  transport-guarantee). -->
  <servlet>
    <servlet-name>FinalizePurchaseServlet</servlet-name>
    <servlet-class>hotdotcom.FinalizePurchaseServlet</servlet-class>
  </servlet>
  
  <!-- A servlet that redirects users to the home page. -->
  <servlet>
    <servlet-name>Redirector</servlet-name>
    <servlet-class>hotdotcom.RedirectorServlet</servlet-class>
  </servlet>
  
  <!-- Associate previously named servlet with custom URL. -->
  <servlet-mapping>
    <servlet-name>FinalizePurchaseServlet</servlet-name>
    <url-pattern>/ssl/FinalizePurchase</url-pattern>
  </servlet-mapping>
  
  <!-- Turn off invoker. Send requests to index.jsp. -->
  <servlet-mapping>
    <servlet-name>Redirector</servlet-name>
    <url-pattern>/servlet/*</url-pattern>
  </servlet-mapping>
  
  <!-- If URL gives a directory but no filename, try index.jsp
  first and index.html second. If neither is found,
  the result is server-specific (e.g., a directory
  listing). -->
  <welcome-file-list>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
  <!-- Protect everything within the "investing" directory. -->
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Investing</web-resource-name>
      <url-pattern>/investing/*</url-pattern>
    </web-resource-collection>
    <auth-constraint>
      <role-name>registered-user</role-name>
      <role-name>administrator</role-name>
    </auth-constraint>
  </security-constraint>
    
  <!-- URLs of the form http://host/webAppPrefix/ssl/blah
  require SSL and are thus redirected to
  https://host/webAppPrefix/ssl/blah. -->
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Purchase</web-resource-name>
      <url-pattern>/ssl/*</url-pattern>
    </web-resource-collection>
    <auth-constraint>
      <role-name>registered-user</role-name>
    </auth-constraint>
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
  
  <!-- Only users in the administrator role can access
  the delete-account.jsp page within the admin
  directory. -->
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Account Deletion</web-resource-name>
      <url-pattern>/admin/delete-account.jsp</url-pattern>
    </web-resource-collection>
    <auth-constraint>
      <role-name>administrator</role-name>
    </auth-constraint>
  </security-constraint>
  
  <!-- Tell the server to use form-based authentication. -->
  <login-config>
    <auth-method>FORM</auth-method>
    <form-login-config>
      <form-login-page>/admin/login.jsp</form-login-page>
      <form-error-page>/admin/login-error.jsp</form-error-page>
    </form-login-config>
  </login-config>
</web-app>
```
#### The Password File
The password file used by Tomcat for this Web application `your_tomcat_dir/conf/tomcat-users.xml`.
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<tomcat-users>
  <user name="john" password="nhoj" roles="registered-user" />
  <user name="jane" password="enaj" roles="registered-user" />
  <user name="juan" password="nauj" roles="administrator" />
  <user name="juana" password="anauj" roles="administrator,registered-user" />
</tomcat-users>
```
#### The Login and Login-Failure Pages
This Web application uses form-based authentication. Attempts by not-yet-authenticated users to access any password-protected resource will be sent to the login.jsp page in the admin directory.

admin/login.jsp file:
```html
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<html>
<head>
 <title>log in</title>
 <link rel=stylesheet href="../company-styles.css" type="text/css">
</head>
<body>
  <h1 class="title">log in</h1>
  <h3>sorry, you must log in before accessing this resource.</h3>
  <form action="j_security_check" method="post">
  <table>
   <tr><td>user name: <input type="text" name="j_username"></td></tr>
   <tr><td>password: <input type="password" name="j_password"></td></tr>
   <tr><td><input type="submit" value="log in"></td></tr>
  </table>
 </form>
</body>
</html>
```
admin/login-error.jsp file:
```html
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<html>
<head>
 <title>begone!</title>
 <link rel=stylesheet href="../company-styles.css" type="text/css">
</head>
<body>
 <h1>begone!</h1>
 <h3>begone, ye unauthorized peon.</h3>
</body>
</html>
```
#### The investing Directory
The web.xml file for this demo app specifies that all URLs that begin with http://host/hotdotcom/investing/ should be password protected, accessible only to users in the registered-user role. The system uses some variation of session tracking to remember which users have previously been authenticated.

investing/index.html file:
```html
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<html>
<head>
 <title>investing</title>
 <link rel=stylesheet href="../company-styles.css" type="text/css">
</head>
<body>
 <h1>Investing</h1>
 <h3><i>hot-dot-com.com</i> welcomes the discriminating investor!</h3>
  please choose one of the following:
 <ul>
  <li><a href="../ssl/buy-stock.jsp">buy stock</a>. Astronomic growth rates!</li>
  <li><a href="account-status.jsp">check account status</a>. See how much you've already earned!</li>
 </ul>
</body>
</html>
```
#### The admin Directory
URLs in the admin directory are not uniformly protected as are URLs in the investing directory. A user in the administrator role can access the page without difficulty.

admin/delete-account.jsp file:
```html
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<html>
 <head>
 <title>delete account</title>
 <link rel=stylesheet href="../company-styles.css" type="text/css">
</head>
<body>
 <h1>delete account</h1>
 <form action="confirm-deletion.jsp">
  username: <input type="text" name="username"><br>
  <center><input type="submit" value="confirm deletion"></center>
 </form>
</body>
</html>
```
