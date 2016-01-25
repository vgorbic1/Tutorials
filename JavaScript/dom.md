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
To change the element on the page use the following methods:
```javascript
.innerHTML    // create element
.removeChild  // remove element
.appendChild  // add element
.replaceChild // replace element
.write        // write into the object
```

