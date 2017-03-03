##Thymeleaf Fragmenting (Refactoring)
- Have a complete HTML place holder file (index.html) that you need to fragment.
- Make sure the file has Thymeleaf ns reference:
```xml
<html lang="en" xmlns:th="html://www.thymeleaf.org">
```
- To fragment the <head> segment, copy all code includint <head> tags.
- Create a new HTML file (header.html). Make sure it has Thymeleaf reference.
```xml
<!DOCTYPE html>
<html lang="en" xmlns:th="html://www.thymeleaf.org">
<head>
</head>
<body>
</body>
</html>
```
- Replace entire <head> element with the one from the clipboard.
- Add the following code to <head> element to link the fragment with index page:
```xml
<head th:fragment="common-header">
```
- In header.html remove <body> element completely and replace it with the script element(s) from 
index.html that are located right before closing <body> element:
```xml
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org">
<head th:fragment="common-header">
<title>DevOps Buddy</title>
<link th:href="@{/webjars/bootstrap/3.3.6/css/bootstrap.min.css}"
	rel="stylesheet" />
<link th:href="@{/css/style.css}" rel="stylesheet" />
</head>
<div th:fragment="before-body-scripts">
	<script th:src="@{/webjars/jquery/2.1.4/jquery.min.js}"></script>
	<script th:src="@{/webjars/bootstrap/3.3.6/js/bootstrap.min.js}"></script>
	<script th:src="@{/js/devopsbuddy.js}"></script>
</div>
</html>
```
- In the index file remove all from <head> element and replace it with:
```xml
<head th:replace="common/header :: common-header" />
```
here *common/header* is the path to the *header* page, and *common-header* is the fragment name.
- Place a div element into index.html placeholder and include a reference to the header.html *before-body-scripts* fragment:
```xml
<div th:replace="common/header :: before-body-scripts" />
```
- Copy navigation bar code from index.html including the top div element.
- Create a new navbar.html file:
```xml
<!DOCTYPE html>
<html lang="en" xmlns:th="html://www.thymeleaf.org">
<head>
</head>
<body>
</body>
</html>
```
- Completely remove the <head> element from the havbar.html.
- Within the <body> element paste the code from clipboard (navigation bar from index.html code). Keep indentation.
- Add reference (th:fragment="common-navbar") to the top <div> element:
```xml
...
<div th:fragment="common-navbar" class="navbar navbar-inverse navbar-fixed-top" role="navigation">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target=".navbar-collapse">
        <span class="sr-only">
...
```
- In the index.php insert this code instead the navbar code:
```xml
...
<body>
  <div th:replace="common/navbar :: common-navbar" />
...
```
