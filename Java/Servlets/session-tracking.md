## Session Tracking
HTTP doesn't maintain state, it is known as a stateless protocol. In contrast, FTP maintains state between requests so it is known as a stateful protocol. Since HTTP is a stateless protocol, Session Tracking is needed to add state back to HTTP. Session Tracking lets us keep track of user data as they navigate our web applications.

#### Other Ways of Session Tracking
- Using hidden form fields is a very early attempt to do session tracking. All site navigation had to go through form submissions and a session was lost if users clicked on regular links.
- URL Rewriting allowed to append a session ID to the end of all URLs of a site dynamically. It works well and the site does not lose track of user sessions, but this technology requires lots of server side coding.
- Cookies allow to store a session ID in the browser. This is overall the best solution.

By default, the servlet API uses a cookie to store the session ID within the client's browser. This is an extension of the HTTP protocol. Then, when the next request is made, this cookie is added to the request. However, if cookies have been disabled within a browser, this type of session tracking won't work.

A *per-session cookie* is stored on the browser until the user closes the browser and a *persistent* cookie can be stored on the user's hard disk for up to 3 years. The session tracking code presented in this chapter relies on per-session cookies. As a result, per-session cookies must be enabled in the user's browser for this to work.

#### Session Tracking in Servlets
HttpSession is used for session tracking. To access the current session object:
```java
HttpSession session = request.getSession();
```
To look up information associated with the session:
```java
session.getAttribute("attribute_name");
```
To store information in a session:
```java
session.setAttribute("attribute_name", <object>);
```
To remove session data:
```java
session.removeAttribute("attribute_name");
```

**Examples:**

Getting an Attribute Servlet
```java
public void doGet(HttpServletRequest request, HttpServletResponse 
        response) throws ServletException, IOException {  
    response.setContentType("text/html");
    PrintWriter  out          = response.getWriter();
    HttpSession  session      = request.getSession();
    String       sessionName  = 
                (String) session.getAttribute("session_name");
    out.print("<html><head></head><body><h3>Getting a "
                + "session in a Servlet</h3><h4>"); 
    if (sessionName == null || sessionName.equals("")) {
        out.print("Attribute not found");
    }
    else {
        out.print("Attribute found: ");
        out.print(sessionName);
    }
        out.print("</body></html>");
}
```
Getting and setting attributes in the session:
```java
public void doGet(HttpServletRequest request, HttpServletResponse 
        response) throws ServletException, IOException {
    response.setContentType("text/html");
    PrintWriter  out          = response.getWriter();
    HttpSession  session      = request.getSession();
    String myAttribute  = (String) session.getAttribute("myAttribute");
    out.print("<html><head></head><body><h3>Getting and "
                + "Setting a session attribute in a Servlet</h3><h4>");
    if (myAttribute == null || myAttribute.equals("")) {
        out.print("myAttribute not found, creating myAttribute");
        session.setAttribute("myAttribute", 
                    "This is a session attribute");
    } else {
        out.print("myAttribute found: ");
        out.print(myAttribute);
    } 
    out.print("</body></html>");
}
```
#### Session tracking in JSP
```xml
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<!DOCTYPE html>
<html>
  <head>
    <title>Session Attributes</title>
  </head>
  <body> 
    <h3>getting an attribute from a session</h3> 
    <c:if test="${session_name != null}" >
       <h3>session_name found: ${session_name}</h3>
    </c:if>
    <c:if test="${session_name == null}" >
       <h3>session_name not found</h3>
    </c:if>
    <c:set var="session_name" value="Hi mom!" scope="session" />
    <p>After: ${session_name}</p>  
  </body>
</html>
```
