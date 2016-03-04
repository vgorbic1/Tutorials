## AJAX Integration
Use serverside code as a single piece of data, that will be handled by JavaScript. The serverside code may be written in PHP outputing a string:
```PHP
<?php
  echo "hello";
?>
```
as an xml string:
```PHP
<?php
  header('Content-type: application/xml');
  $output = "<users><user><id>1</id><name>bill</name></user><user><id>2</id><name>steve</name></user></users>";
  echo $output;
?>
```
as a JSON:
```PHP
<?php
  header('Content-type: application/json');
  $users = array(); 
  $users[] = array("id"=>1, "name"=>"bill");
  $users[] = array("id"=>2, "name"=>"steve");
  echo json_encode($users);
?>
```

#### Integration
Create an HTML file with three buttons representing each datatype (string, XML, and JSON):
```html
<html>
<head>
	<meta http-equiv="Content-type" content="text/html; charset=utf-8">
	<title>DataTypes in AJAX</title>
	<script src="ajaxDataTypes.js" type="text/javascript" charset="utf-8"></script>
</head>
<body id="" onload="">
	<input type="button" value="plain text" id="btnPlaintext">
	<br />
	<input type="button" value="xml" id="btnXML">
	<br />
	<input type="button" value="json" id="btnJSON">
</body>
</html>
<script type="text/javascript" charset="utf-8">
  init();
</script>
```
and a JavaScript (ajaxDataTypes.js) file:
```javascript
function makeAJAXRequest(url, callback) {
	var xhr = new XMLHttpRequest();
	xhr.open("GET", url);
	xhr.onreadystatechange = function() {
		if (xhr.readyState == 4 && xhr.status == 200) {
			callback(xhr);				
		}
	}
	xhr.send(null);
}

function init() {
	var plainTextButton = document.getElementById("btnPlaintext");
	var xmlButton = document.getElementById("btnXML");
	var jsonButton = document.getElementById("btnJSON");		
	
	plainTextButton.onclick = function() {
		makeAJAXRequest("plaintext.php", function(xhr) {
			alert(xhr.responseText);
		})
	}
	
	xmlButton.onclick = function() {
		makeAJAXRequest("xml.php", function(xhr) {
			var names = xhr.responseXML.getElementsByTagName("name");
			for (var i=0; i< names.length; i++) {
				alert(names[i].childNodes[0].nodeValue);
			}
		});
	}
	
	jsonButton.onclick = function() {
		makeAJAXRequest("json.php", function(xhr) {
			var users = eval('(' + xhr.responseText + ')');
			for(var i = 0; i<users.length; i++) {
				alert(users[i].name);
			}
		})
	}
}
```
