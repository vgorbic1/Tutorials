## Events
Events are happen when:
- an element is clicked on
- the page is loaded
- input fields are changed

#### onclick
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
To assign an event using DOM:
```javascript
document.getElementById('button').onclick = function() { displayDate() };
```

#### onload
This event works when user eters the page. It is usually used to check user browser's type or version, as well as whether cookies are disabled.
```javascript
<body onload="checkCookie()">
```
#### onunload
This event works when user leaves the page.

#### onchange
This event is often used in combination with validation of input fields.
```javascript
<input type="text" onchange="upperCase()" />
```

