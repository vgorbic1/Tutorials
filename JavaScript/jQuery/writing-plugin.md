## Authoring Plugins
Example of writing a simple plugin utilizing jQuery library.

#### Create an HTML file
```html
<html>
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
		<script src="jquery.highlighter.js"></script>
		<script src="plugins.js"></script>
	</head>
	<body>
		<ul>
			<li>dogs</li>
			<li>cats</li>
			<li>chickens</li>
		</ul>
		
		<p>asdfjkksadfjksadfjksadfjksadf</p>
		<p>cubs stink</p>
		<p>brewers stink</p>
	</body>
</html>
```
* `jquery.highlighter.js` is a plugin script.
* `plugins.js` local script that uses the `jquery.highlighter.js` plugin
