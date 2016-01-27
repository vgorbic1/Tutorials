## Web Storage
Web storage can store data locally within the user's browser. It is more secure and faster than cookies.
The data is only used when asked for. The storage limit is at least 5 MB. The info in the storage is never
shared with the server. Data is stored in name/value pairs as a string. Convert it to another datatype if needed.

#### Objects for web storage
```javascript
window.localStorage // stores data with no expiration date
window.sessionStorage // stores data for one session only. Data is lost when browser's tab is closed.
```
To create a local storage name/value pair:
```javascript
localStorage.setItem('lastName', 'Smith' );
// or
localStorage.lastName = 'Smith';
```
To get the name/value:
```javascript
document.getElementById('result').innerHtml = localStorage.getItem('lastName'); // insert the pair to the element with id "result"
// or
document.getElementById('result').innerHtml = localStorage.lastName;
```
To remove a name from local storage:
```javascript
localStorage.removeItem("lastName");
```
Same goes with ```sessionStorage```