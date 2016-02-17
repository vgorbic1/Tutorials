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
