## Document Object Model
DOM methods are actions.

DOM properties are values.

All HTML elements are objects.

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

#### Events
Events are happen when:
- an element is clicked on
- the page is loaded
- input fields are changed

**onclick** event
```javascript
<h1 id="header">Header</h1>
<input type="button" onclick="document.getElementById('header').style.color = 'red'" />
```
To call the function from a script:
```javascript
<h1 onclick="changeThisHeader(this)">Header</h1>

function changeThisHeader(id) {
  id.innerHTML = 'Another Header';
}
```
