## jQuery
The purpose of jQuery is to make it much easier to use JavaScript on your website. jQuery is a lightweight, "write less, do more", JavaScript library. The jQuery team knows all about cross-browser issues, and they have written this knowledge into the jQuery library. jQuery will run exactly the same in all major browsers, including Internet Explorer 6!

#### Downloading jQuery
* Production version - this is for your live website because it has been minified and compressed
* Development version - this is for testing and development (uncompressed and readable code)
```javascript
<head>
  <script src="jquery-1.12.0.min.js"></script> // with local file
</head>

or

<head>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
</head>
```

#### jQuery Syntax
Basic syntax is: `$(selector).action()`

To prevent any jQuery code from running before the document is finished loading (is ready) use:
```javascript
$(document).ready(function(){
   // jQuery methods go here...
});
```
The jQuery team has also created an even shorter method for the document ready event:
```javascript
$(function(){
   // jQuery methods go here...
});
```

#### jQuery Selectors
jQuery selectors allow you to select and manipulate HTML element(s). All selectors in jQuery start with the dollar sign and parentheses: `$()`.
* The element selector: `$("p")`
* The id selector: `$("#yourId")`
* The class selector: `$(".yourClass")`
Other selectors:

|Syntax|	Description	Example |
|---|---|
$("*")	|Selects all elements
$(this)	|Selects the current HTML element
$("p.intro")	|Selects all p elements with class="intro"
$("p:first")	|Selects the first p element
$("ul li:first")	|Selects the first li element of the first ul
$("ul li:first-child")	|Selects the first li element of every ul
$("[href]")	|Selects all elements with an href attribute
$("a[target='_blank']")	|Selects all a elements with a target attribute value equal to "_blank"
$("a[target!='_blank']")|	Selects all a elements with a target attribute value NOT equal to "_blank"
$(":button")|	Selects all button elements and input elements of type="button"
$("tr:even")|	Selects all even tr elements
$("tr:odd")	|Selects all odd tr elements

