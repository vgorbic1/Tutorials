## Object Oriented JavaScript
Java is a functional programming language, not object oriented. There are no classes or scopes in JavaScript.
However, there is a way to implement OO features to JavaScript.

#### Class
To crate a class (or a JavaScript representation of class) use a function definition with uppercase name of the function (Classname):
```javascript
function Dog() {
  var name;  // private instance variable
}
```
To create an istance of the class:
```javascript
var poodle = new Dog();
```
Any variable or function to have a public acces from within a class should have `this.` keyword. To create an accessor to the private variable above, add a public function in the class with reference to the private field:
```javascript
function Dog() {
  var name = 'Sparky';  // private instance variable
  
  this.getName = function() {  // public function
    return name;
  }
}
```
To access the getter from outside the class:
```javascript
var poodle = new Dog();
console.log(poodle.getName());
```
To set a priate field use a function:
```javascript
function Dog() {
  var name = 'Sparky';  // private instance variable
  
  this.getName = function() {  // public function (getter)
    return name;
  }
  
  this.setName = function(value) {  // public function (setter)
    name = value;
  }
  
}
```
To set the name:
```javaScript
var poodle = new Dog();
poodle.setName('Fido');
```
To create a public instance variable within a class, again use the keyword `this.`:
```javascript
function Dog() {
  this.email = 'dog@gmail.com';  // public instance variable
}
```
To access this public variable:
```javaScript
var poodle = new Dog();
console.log(poodle.email);
```
