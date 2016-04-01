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
// people.php
$person1 = array("id"=>1, "name"=>"bill gates");
$person2 = array("id"=>2, "name"=>"bernie sanders");	
$person3 = array("id"=>3, "name"=>"hillary clinton");	
$person4 = array("id"=>4, "name"=>"donald trump");	
$people = array($person1, $person2, $person3, $person4);
echo json_encode($people);
```

#### PHP file with XML output:
```php
// xml.php
$output = "<users><user><id>1</id><name>joe</name></user><user><id>2</id><name>sue</name></user></users>";
header("Content-type:application/xml");
echo $output;
```

#### jQuery file with AJAX:
```javascript
// jqueryAJAX.js
$(document).ready(function() {
  $.get("people.php", function(response) {
    outputPeople(response)
  }, "json");
	
  $.get("xml.php", function(users) {
    var output = $("<div>");
    $(users).find("name").each(function(index, nameNode) {
      output.append($("<p>").text($(nameNode).text()));
    });
    $("body").append(output);
  }, "xml");
})

function outputPeople(people) {
  var list = $("<ul>");
  $(people).each(function(index, current) {
    $("<li>").text(current.name).appendTo(list);	
  });
  list.appendTo($("body"));
}
```
