## Programmatic Security
Declarative security is all well and good. In fact, it is by far the most common
approach to Web application security. But, what if you want your servlets to be completely
independent of any server-specific settings such as password files? Or, what if
you want to let users in various roles access a particular resource but customize the
data depending on the role that they are in? Or, what if you want to authenticate
users other than by requiring an exact match from a fixed set of usernames and passwords?
That’s where programmatic security comes in.

## Combining Container-Managed and Programmatic Security
It would be nice to provide this customization without giving up the convenience
of container-managed security for the usernames, passwords, and roles as would be
required if a servlet or JSP page completely managed its own security. To support this type of hybrid security, the servlet specification provides three methods in `HttpServletRequest`:
- `isUserInRole`. This method determines if the currently
authenticated user belongs to a specified role. For example, given the
usernames, passwords, and roles,
if the client has successfully logged in as user valjean, the following
two expressions would return true.
`request.isUserInRole("lowStatus")`
`request.isUserInRole("nobleSpirited")`
Tests for all other roles would return false. If no user is currently
authenticated (e.g., if authorization failed or if `isUserInRole` is
called from an unrestricted page and the user has not yet accessed a
restricted page), `isUserInRole` returns false. In addition to the
standard security roles given in the password file, you can use the
`security-role-ref` element to define aliases for the standard
roles.
- `getRemoteUser`. This method returns the name of the current user.
For example, if the client has successfully logged in as user valjean,
`request.getRemoteUser()` would return "valjean". If
no user is currently authenticated (e.g., if authorization failed or if
`isUserInRole` is called from an unrestricted page and the user has
not yet accessed a restricted page), `getRemoteUser` returns null.
- `getUserPrincipal.` This method returns the current username
wrapped inside a `java.security.Principal` object. The
Principal object contains little information beyond the username
(available with the `getName` method). So, the main reason for using
`getUserPrincipal` in lieu of getRemoteUser is to be compatible
with preexisting security code (the Principal class is not specific to
the servlet and JSP API and has been part of the Java platform since
version 1.1). If no user is currently authenticated, `getUserPrincipal`
returns null.

It is important to note that this type of programmatic security does not negate the
benefits of container-managed security. With this approach, you can still set up usernames,
passwords, and roles by using your server’s mechanisms. You still use the
login-config element to tell the server whether you are using form-based or
BASIC authentication. If you choose form-based authentication, you still use an
HTML form with an ACTION of j_security_check, a textfield named
j_username, and a password field named j_password. Unauthenticated users are
still automatically sent to the page containing this form, and the server still automatically
keeps track of which users have been authenticated. You still use the
security-constraint element to designate the URLs to which the access
restrictions apply. You still use the user-data-constraint element to specify
that certain URLs require SSL.

#### Security Role References
The `security-role-ref` subelement of servlet lets you define servlet-specific
synonyms for existing role names. This element should contain three possible subelements:
`description` (optional descriptive text), `role-name` (the new synonym),
and `role-link` (the existing security role) in web.xml file:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE web-app PUBLIC
"-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
"http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
<web-app>
<!-- ... -->
<servlet>
  <servlet-name>BookInformation</servlet-name>
  <servlet-class>catalog.BookInfo</servlet-class>
  <security-role-ref>
    <role-name>writer</role-name> <!-- New alias. -->
    <role-link>author</role-link> <!-- Preexisting role. -->
  </security-role-ref>
</servlet>

<servlet>
  <servlet-name>EmployeeInformation</servlet-name>
  <servlet-class>hr.EmployeeData</servlet-class>
  <security-role-ref>
    <role-name>goodguy</role-name> <!-- New. -->
    <role-link>nobleSpirited</role-link> <!-- Preexisting. -->
  </security-role-ref>
  <security-role-ref>
    <role-name>meanie</role-name> <!-- New. -->
    <role-link>meanSpirited</role-link> <!-- Preexisting. -->
  </security-role-ref>
</servlet>
<!-- ... -->
<security-constraint>...</security-constraint>
<login-config>...</login-config>
<!-- ... -->
</web-app>
```

#### Handling All Security Programmatically
In some cases, however, you might want a servlet or
JSP page to be entirely self-contained with no dependencies on server-specific settings
or even web.xml entries. Although this approach requires a lot more work, it
means that the servlet or JSP page can be ported from server to server with much
less effort than with container-managed security. Furthermore, it lets the servlet or
JSP page use username and password schemes other than an exact match to a preconfigured
list.

HTTP supports two varieties of authentication: BASIC and DIGEST. Few browsers
support DIGEST, so let's concentrate on BASIC here.
Here is a summary of the steps involved for BASIC authorization:
1. Check whether there is an Authorization request header.
If there is no such header, go to Step 5.
1. Get the encoded username/password string. If there is an
Authorization header, it should have the following form:
Authorization: Basic encodedData
Skip over the word Basic—the remaining part is the username and
password represented in base64 encoding.
1. Reverse the base64 encoding of the username/password string.
Use the decodeBuffer method of the BASE64Decoder class. This
method call results in a string of the form username:password.
The BASE64Decoder class is bundled with the JDK; in JDK 1.3 it
can be found in the sun.misc package in jdk_install_dir/jre/lib/rt.jar.
