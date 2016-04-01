## jQuery Ajax Example.

#### HTML file:
```html
<html>
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
		<script src="jqueryAJAX.js"></script>
	</head>
	<body>
	</body>
</html>
```

#### PHP file with JSON output:
```php
$person1 = array("id"=>1, "name"=>"bill gates");
$person2 = array("id"=>2, "name"=>"bernie sanders");	
$person3 = array("id"=>3, "name"=>"hillary clinton");	
$person4 = array("id"=>4, "name"=>"donald trump");	
$people = array($person1, $person2, $person3, $person4);
echo json_encode($people);
```
