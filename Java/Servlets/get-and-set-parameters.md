## Get and Set Parameters with Servlets

#### Servlet code that gets text from a text box
```java
String firstName = request.getParameter("firstName");
```

#### Servlet code that determines if a check box is checked
It returns the value or "on" if checked, null otherwise.
```java
String nameCheckBox = request.getParameter("name");
if (nameCheckBox != null) {
    // name was checked
}
```

#### Servlet code that reads and processes multiple values from a list box
It returns the values of the items selected in a list box.
```java
String [] selectedCountries = request.getParameterValues("country");
for (String country : selectedCountries) {
  // code to processes each country
}
```

### Set request Parameters
When you work with request attributes, you should realize that the attributes are reset between requests. As a result, if you store a User object as a request attribute and forward that request to a JSP, that User object is only available to that JSP and isn't available later in the session.

#### How to set a request attribute
```java
User user = new User(firstName, lastName, email);
request.setAttribute ("user", user);
```

#### How to get a request attribute
```java
User user = (User) request.getAttribute ("user");
```
#### How to set a request attribute for a primitive type
```java
int id = 1;
request.setAttribute("id", new Integer(id));
```
#### How to get a request attribute for a primitive type
```java
int id = (Integer) request.getAttribute("id");
```
These methods are most often used in conjunction with a RequestDispatcher object
that's used to forward a request as described in the next figure.
