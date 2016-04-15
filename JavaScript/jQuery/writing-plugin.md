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
    alert("cubs stink");
  });
})
```

