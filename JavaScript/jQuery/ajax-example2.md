## jQuery Ajax Example 2. Passing arguments to server.

#### HTML file:
```html
<html lagng="en">
  <head>
    <meta charset="utf-8">
	<title>Question 26</title>
	<link rel="stylesheet" href="" />
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
	<script src="script.js"></script>
  </head>
  <body>
  <input type="text" name="uName" />
  <button>Submit</button> 
  </body>
</html>
```

#### PHP file with JSON output:
```php
// motd.php
<?php
  $uname = $_REQUEST["name"];
  echo $uname . " message of the day";
?>
```

#### jQuery file with AJAX:
```javascript
// script.js
$(function(){	
	$("button").click(function(){
		$.post("motd.php", {name: $("input").val()}, function(data){
			$("<div>").attr("id", "welcome_message").text(data).appendTo("body");		
		});
	});
});
```
