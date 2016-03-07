## AJAX with Parameters. Server-side PHP
Since we can send parameters with AJAX call, we do not need to use a form on our HTML file.

#### Returning a String
Create an HTML file:
```html
<!DOCTYPE html>
<head>
	<meta http-equiv="Content-type" content="text/html; charset=utf-8">
	<title>Ajax with Parameters</title>
	<script src="parameters.js"></script>
</head>
<body>
	Name:<input type="text" id="txtName">
	<input type="button" value="send ajax parameters" id="btnSend" />
</body>
</html>

<script>init();</script>
```
Create a server-side PHP code:
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
		var params = "?name=" + document.getElementById("txtName").value;
		
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
#### Returning a JSON
Create an HTML file:
```html
<html>
	<head>
		<script type="text/javascript" src="ajaxParameters.js"></script>
	</head>
	<body>
		<form action="doSomething.php" method="get">
			<label for="txtId">Enter the ID to search for</label><input type="text" id="txtId" />
			<br />
			<label for="txtName">Enter the NAME to search for</label><input type="text" id="txtName" />			
			<button type="button" id="btnSearch">Search</button>
		</form>
	</body>
	
</html>

<script type="text/javascript">
init();
</script>
```
Create a server-side PHP code:
```PHP 
<?php # parameters.php
	$id = $_REQUEST["cust_id"];
	// Create JSON:
	$cust = array();
	if($id=="10") {
		$cust["name"] = "joe schmoe";
		$cust["orders"] = array();
		$cust["orders"][] = array("id"=>1, "description"=>"first order ever");
	} else {
		$cust["name"] = "bill gates";	
	}
	echo json_encode($cust);
?>
```
Create a JavaScript (ajaxParameters.js) file that uses GET request:
```javascript
function init() {
	var btn = document.getElementById("btnSearch");
	btn.onclick = ajaxRequestWithParameters;
}

function ajaxRequestWithParameters() {
	var url = "parameters.php";
	var parameters = "?cust_id=" + document.getElementById("txtId").value;
	parameters += "&name=" + document.getElementById("txtName").value;
	var xhr = new XMLHttpRequest();
	xhr.open("get", url + parameters);
	xhr.send(null);
	
	//capture the server response
	xhr.onreadystatechange = function() {
		if(xhr.readyState == 4 && xhr.status == 200) {
			var cust = JSON.parse(xhr.responseText);
			alert(cust.name);
			if(cust.orders) {	
				alert("this customer has orders");
			}
		}
	}
}
```
