## Browser Object Model
BOM allows JavaScript to talk to browser

#### window.
The main object of BOM. Usualy ommited in the script:
```javascript```
window.document.getElementById('demo');
// same thing as
document.getElementById('demo');
```
To change a window size:
```javascript
window.innerHeight // change the window height
window.innerWidth // change the window width
```
To open or close a window:
```javascript
window.open();  // or just open();
window.close();  // or just close();
```

#### window.screen
```screen``` object contains information about the user's screen
```javascript
screen.availableWidth // returns the width of the visitor's screen without interface.
```

#### window.location
This object can get the current URL and redirect the browser to a different page.
```javascript
location.herf // returns the current URL
location.pathname // returns the path name of the URL
location.assign('URL') // loads a new document that has given URL
```

#### window.history
This object contains browser's history.
```javascript
history.back()  // loads the previous URL in the history list
