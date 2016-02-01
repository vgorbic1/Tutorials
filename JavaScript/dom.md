## Document Object Model
Everything in a HTML document is a node. All nodes can be accessed by JavaScript. Nodes have hierarchical relationship: root | parent | child | sibling. DOM methods are actions. DOM properties are values. All HTML elements are objects.
```javascript
document.getElementById('email').innerHTML;
      //|--------method-------| |-property-| 
```
- **getElementById** method looks up for an element on the page with the id as the parameter.
- **innerHTML** property sets or gets the content of the method to which it is attached.

To find an element on the page use the following methods:
```javascript
document.getElementById();
document.getElementsByTagName(); // returns an array of tags found. The
document.getElementsByClassName(); // returns an array of elements of this class
document.forms[]; // name of the form goes inside of []
document.anchors[]; // name of the anchor goes inside of []
document.images[]; // name of the image goes inside of []
document.links[]; // name of the link goes inside of []
```
To change the element on the page:
```javascript
document.getElementById('text').innerHTML = 'another text'
 or
var element = document.getElementById('text');
element.innerHTML = 'another text';
```
To change the value of the attribute:
```javascript
document.getElementById('img').src = 'file.jpg';
```
To change the element style:
```javascript
document.getElementById('text').style.color = 'blue';
```
To add or delete an element on the page use the following methods:
```javascript
document.createElement() // create element
document.removeChild()   // remove element
document.appendChild()   // add element
document.replaceChild()  // replace element
document.write(text)     // write into the object
```

#### Examples
**Append an item in a list:**
```javascript
var node = document.createElement("li");                 // Create a <li> node
var textnode = document.createTextNode("Water");         // Create a text node
node.appendChild(textnode);                              // Append the text to <li>
document.getElementById("myList").appendChild(node);     // Append <li> to <ul> with id="myList"
```
Before appending:
- Coffee
- Tea

After appending:
- Coffee
- Tea
- Water

**Append a new element before a known element without direct reference to a parent:**
```javascript
var node = document.createElement('div');  // Create a <div> node
var textnode = document.createTextNode('Water');         // Create a text node
var mainElement = document.getElementById("main");  // Get a known element with id "main"
mainElement.parentNode.insertBefore(node, mainElement);  // Append the new element right before "main"
```
Before appending:
- Main

After appending:
- Water
- Main

**Create an element with some text and append it to the end of the document body:**
```javascript
var paragraph = document.createElement("p");                        // Create a <p> node
var text = document.createTextNode("This is a paragraph.");    // Create a text node
paragraph.appendChild(text);                                           // Append the text to <p>
document.body.appendChild(paragraph);                  // Add to <body> element
```
**Insert a new element before the first child element of another element:**
```javaScript
var newItem = document.createElement("li");       // Create a <li> node
var textnode = document.createTextNode("Water");  // Create a text node
newItem.appendChild(textnode);                    // Append the text to <li>
var list = document.getElementById("myList");    // Get the <ul> element to insert a new node
list.insertBefore(newItem, list.childNodes[0]);  // Insert <li> before the first child of <ul>
```
Before inserting:
- Coffee
- Tea

After inserting:
- Water
- Coffee
- Tea

**Remove the first element from a list:**
```javascript
var list = document.getElementById("myList");   // Get the <ul> element with id="myList"
list.removeChild(list.childNodes[0]);           // Remove <ul>'s first child node (index 0)
```
Before removing:
- Coffee
- Tea
- Milk

After removing:
- Tea
- Milk
