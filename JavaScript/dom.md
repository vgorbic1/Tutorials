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
document.getElementsByTagName();
document.getElementsByClassName();
document.forms[];
```
To change the element on the page use the following properties:
```javascript
.innerHTML =    // change HTML
.attribute =   // change attribute
.setAttribute(attribute, value) // replacing attribute
.style.property = // change syle
```
To add or delete an element on the page use the following methods:
```javascript
document.createElement() // create element
document.removeChild()   // remove element
document.appendChild()   // add element
document.replaceChild()  // replace element
document.write(text)     // write into the object
```
To add an event handler:
```javascript
document.getElementById('email').onclick = function() { ... }
```
