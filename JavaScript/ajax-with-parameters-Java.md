## Ajax with Parameters (jQuery). Server-side Java
Let JavaScript execute an asynchronous HTTP request and update the HTML DOM tree based on the response data.

#### Returning as a String
Create a `/some.jsp` like below (note: the code doesn't expect the JSP file being placed in a subfolder, if you do so, alter serlvet URL accordingly):
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>SO question 4112686</title>
        <script src="http://code.jquery.com/jquery-latest.min.js"></script>
        <script>
            $(document).on("click", "#somebutton", function() { 
                $.get("someservlet", function(responseText) {   
                    $("#somediv").text(responseText);           
                });
            });
        </script>
    </head>
    <body>
        <button id="somebutton">press here</button>
        <div id="somediv"></div>
    </body>
</html>
```
Create a servlet with a doGet() method:
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String text = "some text";
    response.setContentType("text/plain");  // Set content type of the response so that jQuery knows what it can expect.
    response.setCharacterEncoding("UTF-8"); // You want world domination, huh?
    response.getWriter().write(text);       // Write response body.
}
```
Map it in `web.xml` the old fashioned way:
```xml
<servlet>
    <servlet-name>someservlet</servlet-name>
    <servlet-class>com.example.SomeServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>someservlet</servlet-name>
    <url-pattern>/someservlet/*</url-pattern>
</servlet-mapping>
```
Now open the `http://localhost:8080/context/test.jsp` in the browser and press the button. You'll see that the content of the `div` get updated with the servlet response.

#### Returning List of Strings as JSON
With JSON instead of plaintext as response format you can even get some steps further. First, you'd like to have a tool to convert between Java objects and JSON strings. This example utilizes Google Gson. Download and put its JAR file in `/WEB-INF/lib` folder of your webapplication.

Here's an example which displays List<String> as <ul><li>. Create a servlet:
```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    List<String> list = new ArrayList<String>();
    list.add("item1");
    list.add("item2");
    list.add("item3");
    String json = new Gson().toJson(list);

    response.setContentType("application/json");
    response.setCharacterEncoding("UTF-8");
    response.getWriter().write(json);
}
```
Modify the JavaScript (jQuery) `in /some.jsp`:
```JavaScript
$(document).on("click", "#somebutton", function() {  
    $.get("someservlet", function(responseJson) {  
        var $ul = $("<ul>").appendTo($("#somediv")); // Create HTML <ul> element and append it to HTML DOM element with ID "somediv"
        $.each(responseJson, function(index, item) { // Iterate over the JSON array.
            $("<li>").text(item).appendTo($ul);      // Create HTML <li> element, set its text content with currently iterated item and append it to the <ul>.
        });
    });
});
```
#### Returning Map of Strings as JSON
Here's another example which displays Map<String, String> as <option>:
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    Map<String, String> options = new LinkedHashMap<String, String>();
    options.put("value1", "label1");
    options.put("value2", "label2");
    options.put("value3", "label3");
    String json = new Gson().toJson(options);
    response.setContentType("application/json");
    response.setCharacterEncoding("UTF-8");
    response.getWriter().write(json);
}
```
Modify the JavaScript (jQuery) `in /some.jsp`:
```javascript
$(document).on("click", "#somebutton", function() {                "somebutton", execute the following function...
    $.get("someservlet", function(responseJson) {                 
        var $select = $("#someselect");                           
        $select.find("option").remove();                          
        $.each(responseJson, function(key, value) {               
            $("<option>").val(key).text(value).appendTo($select); // Create HTML <option> element, set its value with currently iterated key and its text content with currently iterated item and finally append it to the <select>.
        });
    });
});
```
also change
```html
<select id="someselect"></select>
```
#### Returning List of Entities as JSON
Here's an example which displays `List<Product>` in a `<table>` where the Product class has the properties `Long id, String name` and `BigDecimal price`. Create the servlet:
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    List<Product> products = someProductService.list();
    String json = new Gson().toJson(products);

    response.setContentType("application/json");
    response.setCharacterEncoding("UTF-8");
    response.getWriter().write(json);
}
```
Modify the JavaScript (jQuery) `in /some.jsp`:
```javascript
$(document).on("click", "#somebutton", function() {        // When HTML DOM "click" event is invoked on element with ID "somebutton", execute the following function...
    $.get("someservlet", function(responseJson) {          // Execute Ajax GET request on URL of "someservlet" and execute the following function with Ajax response JSON...
        var $table = $("<table>").appendTo($("#somediv")); // Create HTML <table> element and append it to HTML DOM element with ID "somediv".
        $.each(responseJson, function(index, product) {    // Iterate over the JSON array.
            $("<tr>").appendTo($table)                     // Create HTML <tr> element, set its text content with currently iterated item and append it to the <table>.
                .append($("<td>").text(product.id))        // Create HTML <td> element, set its text content with id of currently iterated product and append it to the <tr>.
                .append($("<td>").text(product.name))      // Create HTML <td> element, set its text content with name of currently iterated product and append it to the <tr>.
                .append($("<td>").text(product.price));    // Create HTML <td> element, set its text content with price of currently iterated product and append it to the <tr>.
        });
    });
});
```
#### Returning List of Entities as XML
Here's an example which does effectively the same as previous example, but then with XML instead of JSON. When using JSP as XML output generator you'll see that it's less tedious to code the table and all. The servlet:
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    List<Product> products = someProductService.list();

    request.setAttribute("products", products);
    request.getRequestDispatcher("/WEB-INF/xml/products.jsp").forward(request, response);
}
```
jsp file:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<%@page contentType="application/xml" pageEncoding="UTF-8"%>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<data>
    <table>
        <c:forEach items="${products}" var="product">
            <tr>
                <td>${product.id}</td>
                <td><c:out value="${product.name}" /></td>
                <td><fmt:formatNumber value="${product.price}" type="currency" currencyCode="USD" /></td>
            </tr>
        </c:forEach>
    </table>
</data>
```
Modify the JavaScript (jQuery) `in /some.jsp`:
```javascript
$(document).on("click", "#somebutton", function() {             
    $.get("someservlet", function(responseXml) {                // Execute Ajax GET request on URL of "someservlet" and execute the following function with Ajax response XML...
        $("#somediv").html($(responseXml).find("data").html()); // Parse XML, find <data> element and append its HTML to HTML DOM element with ID "somediv".
    });
});
```
