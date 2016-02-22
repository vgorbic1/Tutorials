## Declarative Security
Two major aspects to securing Web applications:
- Preventing unauthorized users from accessing sensitive data. This process involves access restriction (identifying which resources
need protection and who should have access to them) and authentication (identifying users to determine if they are one of the authorized
ones).
- Preventing attackers from stealing network data while it is in transit. This process involves the use of Secure Sockets Layer (SSL)
to encrypt the traffic between the browser and the server.

**Declarative security** means that none of the individual servlets or JSP pages need any security-aware code. Instead, both of the major security aspects are handled
by the server.

To prevent unauthorized access, you use the Web application deployment descriptor (web.xml) to declare that certain URLs need protection.
You also designate the authentication method that the server should use to identify users. At request time, the server automatically
prompts users for usernames and passwords when they try to access restricted resources, automatically checks the results against a predefined set of usernames and passwords, and automatically keeps track of which users have previously been authenticated. This process is completely transparent to the servlets and JSP pages.

To safeguard network data, you use the deployment descriptor to stipulate that certain URLs should only be accessible with SSL. If users
try to use a regular HTTP connection to access one of these URLs, the server automatically redirects them to the HTTPS (SSL) equivalent.

#### Form-based Authentication
The most common type of declarative security uses regular HTML forms. The developer uses the deployment descriptor to identify the protected resources and to designate a page that has a form to collect usernames and passwords. If the login is successful and the user belongs to a role that is permitted access to the page, the user is granted access to the page originally requested. If the login is unsuccessful, the user is sent to a designated error page.

Depending on your server, form-based authentication might fail when you use URL rewriting as the basis of session tracking.

#### Setting up Usernames, Passwords, and Roles (Tomcat)
When a user attempts to access a protected resource in an application that is using form-based authentication, the system uses an HTML form to ask for a username and password, verifies that the password matches the user, determines what abstract roles (regular user, administrator, executive, etc.) that user belongs to, and sees whether any of those roles has permission to access the resource. If so, the server redirects the user to the originally requested page. If not, the server redirects the user to an error page.

Although you would not have to change the web.xml file or any of the actual servlet and JSP code to move a secure Web application
from system to system, you would still have to make custom changes on each system to set up the users and passwords.

Tomcat stores usernames, passwords, and roles in `install_dir/conf/tomcat-users.xml`. Each user element should have three attributes: name (the username), password (the plain text password), and roles (a comma-separated list of logical role names). For example:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<tomcat-users>
<user name="valjean" password="forgiven"
roles="lowStatus,nobleSpirited" />
<user name="bishop" password="mercy"
roles="lowStatus,nobleSpirited" />
<user name="javert" password="strict"
roles="highStatus,meanSpirited" />
<user name="thenardier" password="grab"
roles="lowStatus,meanSpirited" />
</tomcat-users>
```
Tomcat's strategy of storing unencrypted passwords is a poor one. Passwords should be encrypted with an algorithm that cannot easily be reversed. For real applications you’ll want to replace the simple file-based password scheme with something more robust. 

#### Designating Locations of Login and Login-Failure Pages
You use the login-config element in the deployment descriptor (web.xml) to control the authentication method.
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE web-app PUBLIC
"-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
"http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
<web-app>
<!-- ... -->
<security-constraint>...</security-constraint>
<login-config>
  <auth-method>FORM</auth-method>
  <form-login-config>
    <form-login-page>/login.jsp</form-login-page>
    <form-error-page>/login-error.html</form-error-page>
  </form-login-config>
</login-config>
<!-- ... -->
```
#### Creating the Login Page
All the login page requires is a form with an ACTION of j_security_check, a textfield named `j_username`, and a password field named `j_password`. All forms that have password fields should use a METHOD of POST. Note that j_security_check is a “magic” name; you don’t preface it with a slash even if your login page is in a subdirectory of the main Web application directory.
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Login</title>
  </head>
  <body>
    <form action="j_security_check" method="post">
      <table>
        <tr><td>user name: <input type="text" name="j_username">
        <tr><td>password: <input type="password" name="j_password">
        <tr><th><input type="submit" value="log in">
      </table>
    </form>
  </body>
</html>
```
#### Creating the Page to Report Failed Login Attempts
What is required to be in the login-failure page? Nothing! This page is arbitrary; it can contain a link to an unrestricted section of the Web application, a link to the login page, or a simple “login failed” message.

#### Specifying URLs That Should Be Password Protected
The security-constraint element should come immediately before login-config in web.xml and contains four possible subelements: display-name (an optional element giving a name for IDEs to use), web-resource-collection (a required element that specifies the URLs that should be protected), authconstraint (an optional element that designates the abstract roles that should have access to the URLs), and user-data-constraint (an optional element that specifies whether SSL is required). Note that multiple web-resource-collection entries are permitted within security-constraint.
```xml
<web-app>
  <!-- ... -->
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Sensitive</web-resource-name>
      <url-pattern>/sensitive/*</url-pattern>
    </web-resource-collection>
    <auth-constraint>
      <role-name>administrator</role-name>
     <role-name>executive</role-name>
    </auth-constraint>
  </security-constraint>
  <login-config>...</login-config>
  <!-- ... -->
</web-app>
```
Each security-constraint element must contain one or more `web-resource-collection` entries; all other securityconstraint
subelements are optional. The` web-resource-collection` element consists of a `web-resource-name` element that gives an arbitrary
identifying name, a `url-pattern` element that identifies the URLs that should be protected, an optional `http-method` element that designates the HTTP commands to which the protection applies (GET, POST, etc.; the default is all methods), and an optional description element providing documentation.
```xml
<security-constraint>
  <web-resource-collection>
    <web-resource-name>Proprietary</web-resource-name>
    <url-pattern>/proprietary/*</url-pattern>
  </web-resource-collection>
  <web-resource-collection>
    <web-resource-name>Account Deletion</web-resource-name>
    <url-pattern>/admin/delete-account.jsp</url-pattern>
  </web-resource-collection>
<!-- ... -->
</security-constraint>
```
It is important to note that the `url-pattern` applies only to clients that access the resources directly. In particular, it does not apply to pages that are accessed through the MVC architecture with a RequestDispatcher or by the similar means of `jsp:forward` or `jsp:include`.

Whereas the `web-resource-collection` element designates the URLs that should be protected, the `auth-constraint` element designates the users that should have access to protected resources. It should contain one or more `role-name` elements identifying the class of users that have access and, optionally, a `description` element describing the role.
```xml
<security-constraint>
  <web-resource-collection>...</web-resource-collection>
  <auth-constraint>
    <role-name>administrator</role-name>
    <role-name>kahuna</role-name>
  </auth-constraint>
</security-constraint>
```
#### Specifying URLs That Should Be Available Only with SSL
Use of SSL does not change the basic way that form-based authentication works. Regardless of whether you are using SSL, you use the login-config element to indicate that you are using form-based authentication and to identify the login and login-failure pages.
In addition to simply requiring SSL, the servlet API provides a way to stipulate that users must authenticate themselves with client certificates.

[EXAMPLE](https://github.com/vgorbic1/Tutorials/blob/master/Java/security-declarative-demo.md)
