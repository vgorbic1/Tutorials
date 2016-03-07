## AJAX with Parameters
Since we can send parameters with AJAX call, we do not need to use a form on our HTML file.
Create an HTML file:
```html
<html>
<head>
	<meta http-equiv="Content-type" content="text/html; charset=utf-8">
	<title>Page Title</title>
	<script src="parameters.js" type="text/javascript" charset="utf-8">
		
	</script>
</head>
<body id="" onload="">
	Name:<input type="text" id="txtName">
	<input type="button" value="send ajax parameters" id="btnSend" />
</body>
</html>

<script type="text/javascript" charset="utf-8">
	init();
</script>
```
Create a serverside PHP code:
```PHP
<?php # parameters.php
// Use $_REQUEST superglobal if you do not now will it be POST or GET request
echo 'hello ' . $_REQUEST["name"];
?>
```
Create the following JavaScript file (parameters.js) if you need to POST data, meaning the server state will change.
```javascript
function init() {
	var btn = document.getElementById("btnSend");
	
	btn.onclick = function() {
		var xhr = new XMLHttpRequest();
		var url = "parameters.php";
		var params = "id=1&name=" + document.getElementById("txtName").value;
		
		xhr.open("POST", url);
		xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
		
		xhr.onreadystatechange = function() {
			if(xhr.readyState == 4 &&
				xhr.status == 200) {
					alert(xhr.responseText);
			}
		}
		
		xhr.send(params);
	}
}
```
Create the following JavaScript file (parameters.js) if you need to GET data, meaning the server state will NOT change.
```javascript
function init() {
	var btn = document.getElementById("btnSend");
	
	btn.onclick = function() {
		var xhr = new XMLHttpRequest();
		var url = "parameters.php";
		var params = "?id=1&name=" + document.getElementById("txtName").value;
		
		xhr.open("GET", url + params);
		
		xhr.onreadystatechange = function() {
			if(xhr.readyState == 4 &&
				xhr.status == 200) {
					alert(xhr.responseText);
			}
		}
		
		xhr.send(null);
	}
}
```
