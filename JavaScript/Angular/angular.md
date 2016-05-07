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
