## JSP
A JSP page is an HTML page with embedded Java code. JSP file is generated into a servlet and then got compiled. In other words, JSP is a way to write servlets.

#### Scripting Elements
The static HTML text in an JSP file is known as template text. Scripting elements let you embed Java code in an HTML document. Tomcat (container) wraps every JSP page in a class of type Servlet behind the scenes. 

**Comments**

The JSP comments between <%--  and  --%> are NOT passed to the browser. At translation time they are stripped from the code and don’t even appear in the generated servlet file:
```
<%-- A JSP Comment --%>
```

**Expressions**

An expression scripting element inserts into the page the result of an Java expression enclosed into <%= and %> The expression is not a Java statement and has no semicolon at the end! 
```
<%= new java.util.Date() %>
```
Expressions are frequently used with predefined variables (Implicit objects). JSP expressions become print (or write) statements in the servlet that results from the JSP page. Whereas regular HTML becomes print statements with double quotes around the text, JSP expressions become print statements with no double quotes. It is similar to:
```java
out.print( new java.util.Date() );
```
XML authors can use the following alternative syntax for JSP expressions (but do not mix both ways in one page):
```
<jsp:expression> new java.util.Date() </jsp:expression>
```
This means that, to use the XML version, you must use XML syntax in the entire page. In JSP 1.2 (but not 2.0), this requirement means that you have to enclose the entire page in a `jsp:root` element. Note that XML elements, unlike HTML ones, are case sensitive. So, be sure to use `jsp:expression` in lower case.

**Scriplets**

A scriptlet is a block of Java code enclosed between <% and %> A JSP scriptlet is used to run arbitrary java code on the JSP page:
```
<%
    String greeting = "Well hi there!";
    out.println(greeting);
%>
```
In general, however, scriptlets can perform a number of tasks that cannot be accomplished with expressions alone. These tasks include setting response headers and status codes, invoking side effects such as writing to the server log or updating a database, or executing code that contains loops, conditionals, or other complex constructs. The scriptlet code is just directly inserted into the `_jspService` method: no strings, no print statements, no changes whatsoever.
The XML equivalent of a scriptlet code is:
```xml
<jsp:scriptlet> out.println(greeting); </jsp:scriptlet>
```
Another use of scriptlets is to conditionally output HTML or other content that is not within any JSP tag. Scriptlets need not contain complete Java statements and that code blocks left open can affect the static HTML or JSP outside the scriptlets:
```
<% if (Math.random() < 0.5) { %>
<H1>Have a <I>nice</I> day!</H1>
<% } else { %>
<H1>Have a <I>lousy</I> day!</H1>
<% } %>
```

**Declarations**

A declaration scripting element is a Java variable declaration enclosed in <%! and %>. A JSP declaration lets you define method or fields that are being inserted into the main body of the servlet class. This code is placed outside of the service method.
```
<%! private String greeting = "Hello again!"; %>
```
In principle, JSP declarations can contain field (instance variable) definitions, method definitions, inner class definitions, or even static initializer blocks: anything that is legal to put inside a class definition but outside any existing methods. However, declarations almost always contain field or method definitions. Do not use JSP declarations to override the standard servlet life-cycle methods (service, doGet, init, etc.). For initialization and cleanup, you can use `jspInit` and `jspDestroy` — the standard init and destroy methods are guaranteed to call these two methods in servlets that come from JSP. If you declare a method name `jspInit()` it will be called once when the JSP page is first loaded and before the request is passed to the page:
```
<%!
    public void jspInit() {
        //initialization code here
    } 
%>
```
The XML equivalent of declaration is:
```xml
<jsp:declaration>
    public void jspInit() {
        //initialization code here
    } 
 </jsp:declaration>
```

**Directives**

A directive element passes to Tomcat data about themselves. This data influences the translation process from a script file to a Java servlet class. As directives only play a role when a JSP page is re-compiled after you modify it, they have no specific effect on the individual HTML responses.

*Page Directive:*

The page directive defines several page-dependent properties expressed through attributes. These properties should appear only once in a JSP page (unless the multiple instances all have the same value, but why should you do that?). You can write more than one page directive in a JSP page, and they will all apply. Their order or position within the page is generally irrelevant.
```
<%@page language="java" contentType="text/html"%>
```
This is usually followed by one or more page directives to tell Tomcat which external class definitions your code needs:
```
<%@page import="java.util.ArrayList"%>
<%@page import="java.util.Iterator"%>
<%@page import="myBeans.OneOfMyBeans"%>
```
or just:
```
<%@page import="java.util.ArrayList, java.util.Iterator"%>
```
It is not good coding practice to import whole class libraries, as in
```
<%@page import="java.util.*"%>
```
The import attribute of the page directive lets you specify the packages that should be imported by the servlet into which the JSP page gets translated. Using separate utility (helper) classes makes your dynamic code easier to write, maintain, debug, test, and reuse. When you use utility classes, remember that they should always be in packages. For one thing, packages are a good strategy on any large project because they help protect against name conflicts. With JSP, however, packages are absolutely required. 
Use of the import attribute takes one of the following two forms.
```
<%@ page import="package.class" %>
<%@ page import="package.class1,...,package.classN" %> 
```
The contentType attribute sets the Content-Type response header, indicating the MIME type of the document being sent to the client.
```
<%@ page contentType="MIME-Type" %>
<%@ page contentType="MIME-Type; charset=Character-Set" %>
```
The session attribute controls whether the page participates in HTTP sessions. Use of this attribute takes one of the following two forms:
```
<%@ page session="true" %> <%-- Default --%>
<%@ page session="false" %>
```
The info attribute defines a string that can be retrieved from the servlet by means of the getServletInfo method. Use of info takes the following form.
```
<%@ page info="Some Message" %>
```
The errorPage attribute specifies a JSP page that should process any exceptions (i.e., something of type Throwable) thrown but not caught in the current page:
```
<%@ page errorPage="/WEB-INF/SpeedErrors.jsp" %>
```
The exception thrown will automatically be available to the designated error page by means of the exception variable.
If you are writing XML-compatible JSP pages, you can use an alternative XML-compatible syntax for directives as long as you don’t mix the XML syntax and the classic syntax in the same page:
```xml
<jsp:directive.page import="java.util.*" />
```

*Include Directive:*

The include directive lets you insert into a JSP page the unprocessed content of another text file:
```
<%@include file="some_jsp_code.jspf"%>
```
JSPF stands for JSP Fragment, although more recently, chunks of JSP code have been called JSP Segments, rather than Fragments. In fact, any text file with any extension will do. For file inclusion, use jsp:include whenever possible (described below). Reserve the include directive (<%@ include ... %>) for cases in which the included file defines fields or methods that the main page uses or when the included file sets response headers of the main page.

*The Taglib Directive:*

You can extend the number of available JSP tags by directing Tomcat to use external self-contained tag libraries. The taglib directory identifies a tag library and specifies what prefix you use to identify its tags:
```
<%@taglib uri="http://mysite.com/mytags" prefix="my"%>
```
This makes possible to write the following line as part of your JSP page:
```
<my:oneOfMyTags> ... </my:oneOfMyTags>
```

*Include Action*

The `jsp:include` action is one of the JSP constructs that has only XML syntax, with no equivalent “classic” syntax. The jsp:include action includes the output of a secondary page at the time the main page is requested. Although the output of the included pages cannot contain JSP, the pages can be the result of resources that use servlets or JSP to create the output. That is, the URL that refers to the included resource is interpreted in the normal manner by the server and thus can be a servlet or JSP page. The server runs the included page in the usual way and places the output into the main page. This is precisely the behavior of the include method of the RequestDispatcher class, which is what servlets use if they want to do this type of file inclusion. Relative URLs that do not start with a slash are interpreted relative to the location of the main page. Relative URLs that start with a slash are interpreted relative to the base Web application directory, not relative to the server root. The jsp:include action never causes the system to look at files outside of the current Web application:
```xml
<jsp:include page="bios/cheng-yinghua.jsp" />
<jsp:include page="/templates/footer.jsp" />
```
To prevent the included files from being accessed separately, place them in WEB-INF or a subdirectory thereof.

**Declaring Variables**

Create variable for each incoming HTTP client request:
```
<% int k = 0; %>
```
Create a variable for each new instance of the servlet:
```
<%! int k = 0; %> 
```
Create a variable that is shared among all instances of the servlet:
```
<%! static int k = 0; %> 
```
Tomcat converts each JSP page into a subclass of the HTTP Servlet class `javax.servlet.http.HTTPServlet` Normally, Tomcat instantiates each one of these classes only once and then creates a new Java thread for each incoming request.

**Implicit Objects**

If you are not sure which class a particular object instantiates use this:
```
<%= object_at_question.getClass().getName()%>
```
- The Application Object: Tomcat uses this object to implement the interface java.servlet.ServletContext. It provide resources shared by the web application.
- The Config Object: Tomcat defines to implement the interface javax.servlet.ServletConfig. Tomcat uses this object to pass information to the servlets.
- The Exception Object: The exception object is an instance of a subclass of Throwable (e.g., java.lang.NullPointerException) and is only available in error pages.
- The Out Object: Use the out object in JSP as you use the System.out object in Java: to write to the standard output.
- To remove all unnecessary spaces from the output, including the newlines:
`<%@page trimDirectiveWhitespaces="true"%>`
- The Request Object: The request variable gives you access within your JSP page to the HTTP request sent to it by the client.
The request variable is of HttpServletRequest type and is also an Attribute Map. An Attribute Map is a map with keys that are strings and values that can be any object. Here are some of the methods we can use with an HttpServletRequest object.
```
setAttribute("key", <value>)
getAttribute("key")
removeAttribute("key")
```
For example:
```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {    
    request.setAttribute("test", "This is just a test!");    
}
```
- To get all parameters from the URL string:
```java
String[] par = request.getParameterValues("par-name");
```
- The Response Object: The response variable gives you access within your JSP page to the HTTP response to be sent back to the client. The HTTP status codes are all between 100 and 599. The range 100–199 is reserved to provide information, 200–299 to report successful completion of the requested operation, 300–399 to report warnings, 400–499 to report client errors, and 500–599 to report server errors.
- The Session Object: The term session refers to all the interactions a client has with a server from the moment the user views the first page of an application to the moment they quit the browser (or the session expires because too much time has elapsed since the last request). The session variable lets your JSP pages store information associated with each individual user:
```java
session.setAttribute("MyAppOperator", "");
```
Then, you can use the following code to check it:
```java
boolean isOperator = (session.getAttribute("MyAppOperator") != null);
if (isOperator) { ...
```

#### The Model 1 Architecture
The simplest way to separate presentation and logic is to move the bulk of the application logic from JSP to Java classes (i.e., Java beans), which can then be used within JSP:

![model1](https://cloud.githubusercontent.com/assets/13823751/13238020/cceea14c-d995-11e5-9fd9-6d726b879866.jpg)

#### The Model 2 Architecture
A better solution, more suitable for larger applications, is to split the functionality further and use JSP exclusively to format the HTML pages. This solution comes in the form of the JSP Model 2 architecture, also known as the model-view-controller (MVC):

![model2](https://cloud.githubusercontent.com/assets/13823751/13238056/fd19d18e-d995-11e5-90ec-f491018984bd.jpg)

With this model, a servlet processes the request, handles the application logic, and instantiates Java beans. JSP obtains data from the beans and can format the response without having to know anything about what’s going on behind the scenes.
