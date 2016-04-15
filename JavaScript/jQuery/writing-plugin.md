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
      <li>one</li>
      <li>two</li>
      <li>three</li>
    </ul>
  </body>
</html>
```
* `jquery.highlighter.js` is a plugin script.
* `plugins.js` local script (plugin driver) that uses the `jquery.highlighter.js` plugin.

#### Create plugin driver file
```javascript
$(document).ready(function() {
  $.fn.highlighter.defaults.color = "blue";
  $("li").highlighter({"color":"red"}).on("click", function() {
    alert("color changed");
  });
})
```

#### Create plugin
```javascript
(function($) {

	$.fn.highlighter = function(options) {
		var localDefaults = $.extend({}, $.fn.highlighter.defaults); // clone defaults
		$.extend(localDefaults, options); // if options exist, use them. Otherwise, use defaults
	
		return $(this).each(function(index, item) { // for each element ...
			console.log("highlighter");  // write this line in console
			$(item).css("backgroundColor", localDefaults.color); // and change the background
		});
	}
	
	$.fn.highlighter.defaults = {"color" : "yellow"}; // create defaults property for the plugin
	
})(jQuery)
```

Put the plugin inside closure (self-calling function), to know that `$` represents jQuery library. Wrapping a function between parenthesis ensures this function to be evaluated as a function expression.
