## Sortable list backed up with database
The app will get a list of items from a database and allow sorting it. The sorted order will be saved to database.

#### Create HTML file
```html
<html>
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
		<link rel="stylesheet" href="https://ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/themes/smoothness/jquery-ui.css">
		<script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/jquery-ui.min.js"></script>
		<script src="sortable.js"></script>
	</head>
	<body>
		<ul id="tasks">
		</ul>
	</body>
</html>
```

## Create JavaScript (jQuery) file and call it `sortable.js`:
```javascript
$(document).ready(function() {
	
	$("#tasks").sortable({ //make the list sortable
		"update":function(event, ui) {  // if sorted, save to database
			$.post("updatePriorities.php", $("#tasks").sortable("serialize")); // send JSON (array of ids in new order)
		}
	});
	
	$.get("allTasks.php", function(tasks) {  // display list
		$(tasks).find("task").each(function(index, task) {
			var id = $(task).find("id").text();
			var desc = $(task).find("description").text();
			$("<li>").attr("id", "task_" + id).text(desc).appendTo($("#tasks"));
		});
		
	}, "xml");
})
```

#### Create server-side script `updatePriorities.php`:
```php
<?php
    $userName = "root";
    $password = "";
    $dbName = "ToDo";
    $server = "localhost";
    $db = new mysqli($server, $userName, $password, $dbName);
    $sql = "update tasks set current_priority = ? where id = ?";
    $stmt = $db->prepare($sql);
    
	foreach($_POST["task"] as $priority=>$id) { // get 'priority' and 'id' of each element
		$stmt->bind_param("ii", $priority, $id);
		$stmt->execute();
	}
    
    $returnVal = $stmt->affected_rows;
    $stmt->close();
    $db->close();
    echo $returnVal;
?>
```

#### Database:
* Database name: `ToDo`
* Connection: "root" ""
* Table: `tasks` (`id` int(11) NOT NULL AUTO_INCREMENT, `description` varchar(500) NOT NULL, `complete` tinyint(1) NOT NULL, `current_priority` int NOT NULL, `created` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP, PRIMARY KEY (`id`)
