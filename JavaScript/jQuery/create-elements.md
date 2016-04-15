## Creating Elements
With jQuery, it is easy to add new elements/content.

#### To create an element:
Use "<>" to create an HTML tag:
```javascript
$("<p>");
// or $("<p></p>");
// same thing as document.createElement("p");
```
To add some content to this new tag use `.text()`:
```javascript
$("<p>").text("appended this text");
```
Now, you need to appned/prepend this element to existing HTML element. Use a temporaty variable and append/prepend that variable to an existing element.

#### append()
The jQuery `append()` method inserts content AT THE END of the selected HTML element:
```javascript
$("p").append("appended this text");
```

#### prepend()
The jQuery `prepend()` method inserts content AT THE BEGINNING of the selected HTML element.
```javascript
$("p").prepend("prepended this text");
```

