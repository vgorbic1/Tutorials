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

