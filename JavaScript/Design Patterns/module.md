## Module Pattern
This pattern helps to break code into separate pieces (modules). ES6 introduced a splecial feature called Modules that solves this problem.

### Basic Structure (Blueprint)
```javascript
(function () {
  // Declare private variables and functions
  return
  // Public variables and functions
})();
```
### Standard Module Pattern
```javascript
const UIController = (function(){
  
  let text = "Hello World";
  
  const changeText() {
    const element = document.querySelector('h1');
    element.textContent = text;
  }
  
  return {
    callChangeText: function () {
      changeText();
      console.log(text)
    }
  }
})();

UIController.callChangeText();  // public
UIController.ChangeText(); // cannot do this. Function is private
```

### Revealing Module Pattern
```javascript
