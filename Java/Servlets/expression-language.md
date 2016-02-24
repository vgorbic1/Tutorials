## Expression Language (EL)
JSP 2.0 introduced a shorthand language for evaluating and outputting the values of Java objects that are stored in standard locations. The JSP expression language cannot be used in servers that support only
JSP 1.2 or earlier.

To permit the JSP page to access the data, the servlet needs to use setAttribute() to store the data in one of the standard locations: the HttpServletRequest, the HttpSession, or the ServletContext. Objects in these locations are known as “scoped variables,” and the expression language has a quick and easy way to access them. You can also have scoped variables stored in the PageContext object, but this is much less useful because the servlet and the JSP page do not share PageContext objects. Thus, page-scoped variables apply only to objects stored earlier in the same JSP page, not to objects stored by a servlet. To output a scoped variable, you simply use its name in an expression language element:
${name}
The expression searches the PageContext, HttpServletRequest, HttpSession, and ServletContext (in that order) for an attribute named "name". If the attribute is found, its toString() method is called and that result is returned. If nothing is found, an empty string (not null or an error message) is returned.

The JSP expression language provides a simple but very powerful dot notation for accessing bean properties. To return the firstName property of a scoped variable named "customer", you merely use:
${customer.firstName}

The expression language lets you nest properties arbitrarily. For example, if the NameBean class had an address property (i.e., a getAddress() method) that returned an Address object with a zipCode property (i.e., a getZipCode() method), you could access this zipCode property with the following simple form.
${customer.address.zipCode}

The expression language lets you replace dot notation with array notation (square brackets). So, for example, you can replace ${name.property} with ${name["property"]}
The second form is rarely used with bean properties. However, it does have two advantages:
First, it lets you compute the name of the property at request time. With the array notation, the value inside the brackets can itself be a variable; with dot notation the property name must be a literal value.
Second, the array notation lets you use values that are illegal as property names. This is of no use when accessing bean properties, but it is very useful when accessing collections or request headers.

Access Collections
The JSP 2.0 expression language lets you access different types of collections in the same way: using array notation. For instance, if attributeName is a scoped variable referring to an array, List, or Map, you access an entry in the collection with the following:
${attributeName[entryName]}
If the scoped variable is an array, the entry name is the index and the value is obtained with theArray[index]. For example, if customerNames refers to an array of strings, to get the first entry in the array you use:
${customerNames[0]}
If the scoped variable is an object that implements the List interface, the entry name is the index and the value is obtained with theList.get(index). For example, if supplierNames refers to an ArrayList, to output the first entry in the ArrayList:
${supplierNames[0]}
If the scoped variable is an object that implements the Map interface, the entry name is the key and the value is obtained with theMap.get(key). For example, if stateCapitals refers to a HashMap whose keys are U.S. state names and whose values are city names, to output "Annapolis"
${stateCapitals["maryland"]}
If the Map key is of a form that would be legal as a Java variable name, you can replace the array notation with dot notation. So, the previous example could also be written as:
${stateCapitals.maryland}
However, note that the array notation lets you choose the key at request time, whereas the dot notation requires you to know the key in advance.

Access Implicit Objects
The pageContext object refers to the PageContext of the current page. The PageContext class, in turn, has request, response, session, out, and servletContext properties (i.e., getRequest, getResponse, getSession,
getOut, and getServletContext methods). So, for example, the following outputs the current session ID:
${pageContext.session.id}
These objects let you access the primary request parameter value (param) or the array of request parameter values (paramValues):
${param.custID}
These objects access the primary and complete HTTP request header values, respectively. Remember that dot notation cannot be used when the value after the dot would be an illegal property name:
${header.Accept} or ${header["Accept"]}
The cookie object lets you quickly reference incoming cookies. However, the return value is the Cookie object, not the cookie value. To access the value, use the standard value property (i.e., the getValue method) of the Cookie class:
${cookie.userCookie.value}
${cookie["userCookie"].value}
The initParam object lets you easily access context initialization parameters:
${initParam.defaultColor}
PageScope, requestScope, sessionScope, and applicationScope: these objects let you restrict where the system looks for scoped variables. For example, with
${name} the system searches for name in the PageContext, the HttpServletRequest, the HttpSession, and the ServletContext, returning the first match it finds. On the other hand, with ${requestScope.name} the system only looks in the HttpServletRequest.

Expression Language Operators
The JSP 2.0 expression language defines a number of arithmetic, relational, logical, and missing-value-testing operators. Avoid using the operators for business logic (creating and processing the data). Instead, put business logic in regular Java classes and invoke the code from the servlet that starts the MVC process.
<TD>\${3+2-1}<TD>${3+2-1} <%-- Addition/Subtraction --%>
<TD>\${1&lt;2}<TD>${1<2} <%-- Numerical comparison --%>
<TD>\${"1"+2}<TD>${"1"+2} <%-- String conversion --%>
<TD>\${"a"&lt;"b"}<TD>${"a"<"b"} <%-- Lexical comparison --%>
<TD>\${1 + 2*3 + 3/4}<TD>${1 + 2*3 + 3/4} <%-- Mult/Div --%>
<TD>\${2/3 &gt;= 3/2}<TD>${2/3 >= 3/2} <%-- >= --%>
<TD>\${3%2}<TD>${3%2} <%-- Modulo --%>
<TD>\${3/4 == 0.75}<TD>${3/4 == 0.75} <%-- Numeric = --%>
<%-- div and mod are alternatives to / and % --%>
<TD>\${(8 div 2) mod 3}<TD>${(8 div 2) mod 3}
<%-- Compares with "equals" but returns false for null --%>
<TD>\${null == "test"}<TD>${null == "test"}
<TD>\${(1&lt;2) && (4&lt;3)}<TD>${(1<2) && (4<3)} <%--AND--%>
<TD>\${empty ""}<TD>${empty ""} <%-- Empty string --%>
<TD>\${(1&lt;2) || (4&lt;3)}<TD>${(1<2) || (4<3)} <%--OR--%>
<TD>\${empty null}<TD>${empty null} <%-- null --%>
<TD>\${!(1&lt;2)}<TD>${!(1<2)} <%-- NOT -%>
<%-- Handles null or empty string in request param --%>
<TD>\${empty param.blah}<TD>${empty param.blah}
<TD BGCOLOR="${(apples.total < 0) ? "RED" : "WHITE" }">

The expression language removes the need for most typecasts and for much of the code that parses strings as numbers. In most cases, missing values or NullPointerExceptions result in empty strings, not thrown exceptions.

These EL elements can appear in ordinary text or in JSP tag attributes, provided that those attributes permit regular JSP expressions. For example:
<UL>
  <LI>Name: ${expression1}
  <LI>Address: ${expression2}
</UL>
<jsp:include page="${expression3}" />

When you use the expression language in tag attributes, you can use multiple expressions (possibly intermixed with static text) and the results are coerced to strings and concatenated. For example:
<jsp:include page="${expr1}blah${expr2}" />
