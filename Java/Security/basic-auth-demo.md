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

