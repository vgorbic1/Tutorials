## HTTP Basic Security
With BASIC security, the browser uses a dialog box instead of an HTML form to collect the username
and password. Then, the Authorization request header is used to remember
which users have already been authenticated. As with form-based security, you
must use SSL if you are concerned with protecting the network traffic. However,
doing so neither changes the way BASIC authentication is set up nor necessitates
changes in the individual servlets or JSP pages.

Compared to form-based authentication, the two main disadvantages of BASIC
authentication are that the input dialog looks glaringly different than the rest of your
application and that it is very difficult to log in as a different user once you are
authenticated. In fact, once authenticated, you have to quit the browser and restart if
you want to log in as a different user!

#### Setting Up Usernames, Passwords, and Roles
This step is exactly the same when BASIC authentication is used as when form-based
authentication is used.

#### Telling the Server You Are Using BASIC Authentication; Designating Realm
You use the login-config element in the deployment descriptor to control the
authentication method. To use BASIC authentication, supply a value of BASIC for
the auth-method subelement and use the realm-name subelement to designate
the realm that will be used by the browser in the popup dialog box and in the
Authorization request header:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE web-app PUBLIC
"-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
"http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
<web-app>
<!-- ... -->
<security-constraint>...</security-constraint>
<login-config>
<auth-method>BASIC</auth-method>
<realm-name>Some Name</realm-name>
</login-config>
<!-- ... -->
</web-app>
```
#### Specifying URLs That Should Be Password Protected
You designate password-protected resources in the same manner with BASIC authentication
as you do with form-based authentication.

#### Specifying URLs That Should Be Available Only with SSL
You designate SSL-only resources in the same manner with BASIC authentication as
you do with form-based authentication.
