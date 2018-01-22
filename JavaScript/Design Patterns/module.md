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
const ItemController = (function(){
  
  let data = [];
  
  function add(item) {
    data.push(item);
    console.log('Item Added...');
  }
  
  function get(id) {
    return data.find(item => {
      return item.id === id;
    });
  }
  
  return {
    add: add,
    get: get
  }
})();

ItemController.add({id: 1, name: 'pen'});
console.log(ItemController.get(2));
```
