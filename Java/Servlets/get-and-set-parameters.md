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
