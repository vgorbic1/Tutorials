## Popup Boxes

#### Alert box
User have to click "OK" to proceed. To make line brake use \n symbol.
```javascript
alert('Hello! \n How are you?');
```

#### Confirm box
User have to click "OK" or "Cancel" to proceed. This box returns true or false boolean.
```javascript
var confirmation = confirm('Proceed?');
if (cofirmation) {
  // proceed
} else {
  // cancel
}
```

#### Prompt box
User have to put in a value and confirm clicking on "OK" or "Cancel". This box returns a value or null.
```javascript
var yourName = prompt('Enter your name', 'John Doe'); // the second parameter is the default value
if (yourName != null) {
  document.getElementById('demo').innerHTML = 'Hello ' + yourName + '!';
}
