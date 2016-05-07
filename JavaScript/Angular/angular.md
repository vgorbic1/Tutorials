## Angular.js

#### Simple example using Angular.js
index.html file:
```html
<!DOCTYPE html>
<html ng-app="demo">
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.9/angular.min.js"></script>
		<script src="app.js"></script>
	</head>
	<body>
		<div ng-controller="matc as mc">
			<ul id="students">
				<li ng-repeat="s in mc.students">
					{{s.id}}. {{s.name}} {{s.email}}
				</li>
			</ul>
			
			<!-- live preview. Render id, name, email -->
			<live-preview></live-preview>
			
			<form ng-submit="mc.addStudent();">
				<div><label for="id">id:</label><input ng-model="mc.student.id" type="text" id="id" /></div>
				<div><label for="name">name:</label><input ng-model="mc.student.name" type="text" id="name" /></div>
				<div><label for="email">email:</label><input ng-model="mc.student.email" type="text" id="email" /></div>
				<input type="submit" value="create new student" />
			</form>
		</div>
	</body>
</html>
```
HTML template to show live privew - live-preview.html
```html
<div>id: {{mc.student.id}}</div>
<div>name: {{mc.student.name}}</div>
<div>email: {{mc.student.email}}</div>
```
Server-side file students.php
```PHP
<?php
$students = array();
$students[] = array("id"=>1, "name"=>"bill", "email"=>"bgates@msn.com");
$students[] = array("id"=>2, "name"=>"steve", "email"=>"sjobs@mac.com");
$students[] = array("id"=>3, "name"=>"jeff", "email"=>"jeff@amazon.com");
header("Content-Type:application/json");
echo json_encode($students);
?>
```
Angular application file app.js
```javascript
(function() {
	var app = angular.module("demo", []);
	
	app.controller("matc", ["$http", function($http) {
		this.students = [];
		
		var myController = this;
		$http.get("students.php").success(function(data) {
			myController.students = data;
		});
		
		this.student = {}; //new student
		this.addStudent = function() {
			
			this.students.push(this.student);
			alert(this.students.length);
			this.student = {};
		}
	}]);
	
	app.directive("livePreview", function() {
		return {
			"templateUrl": "live-preview.html",
			"restrict": "E"
		}
	});
})();
```
