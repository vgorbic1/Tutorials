##Thymeleaf Fragmenting
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
- In header.html remove <body> element completely and replace it with the <script> element(s) from 
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
here "common/header" is the path to the "header" page, and "common-header" is the fragment name.
