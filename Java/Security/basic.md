## HTTP Basic Security
With BASIC security, the browser uses a dialog box instead of an HTML form to collect the username
and password. Then, the Authorization request header is used to remember
which users have already been authenticated. As with form-based security, you
must use SSL if you are concerned with protecting the network traffic. However,
doing so neither changes the way BASIC authentication is set up nor necessitates
changes in the individual servlets or JSP pages.
