## Session Tracking

Since HTTP is a stateless protocol, Session Tracking is needed to add state back to HTTP. Session Tracking lets up keep track of user data as they navigate our web applications.

OTHER WAYS OF SESSION TRACKING
Using hidden form fields is a very early attempt to do session tracking. All site navigation had to go through form submissions and a session was lost if users clicked on regular links.
URL Rewriting allowed to append a session ID to the end of all URLs of a site dynamically. It works well and the site does not lose track of user sessions, but this technology requires lots of server side coding.
Cookies allow to store a session ID in the browser. This is overall the best solution.

SESSION TRACKING IN SERVLETS
HttpSession is used for session tracking:
To access the current session object:
HttpSession session = request.getSession();
To look up information associated with the session:
session.getAttribute("attribute_name");
To store information in a session:
session.setAttribute("attribute_name", <object>);
To remove session data:
session.removeAttribute("attribute_name");

Examples:
Getting an Attribute Servlet
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
Getting and setting attributes in the session
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

SESSION TRACKING IN JSP
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
