## Functions
JavaScript treats function as another datatype along with number, string, etc.
```javascript
init() {
 ...
}
 // is the same as
var init = function() {
 ...
}
```
- A function defenition is global by default.
- A pair of parenthesis with function name mean execute the function right now.
- JavaScript function always has a return type even when no `return` keyword provided (will be "undefined" in this case").

#### Calling a function definition and Anonymous function.
Call one function definition from another function. Check that called function signature has no parameters, because we want to call it only when a user click on button, not when the `init()` function executes.
```javascript
init () {
  var btn = document.getElementById("btn");
  btn.onclick = btnClick;  // No parenthesis
}

btnClick() {
  console.log("button was clicked");
}
```
To call a function definition with parameters:
```javascript
init () {
  var btn = document.getElementById("btn");
  btn.onclick = function() {  // this is called anonymous function
      btnClick("button was clicked"); 
  }
}

btnClick(message) {
  console.log(message);
}
```
If you execute a function in the HTML page the browser automatically will write a function definition for you:
<input type="button" value="message" onclick="show('My message')" />
