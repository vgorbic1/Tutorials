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
#### Adding instances dynamically
In JavaScript, it is possible to add instances on the fly, if you don't have that field in the class definition!
```javascript
var poodle = new Dog();
poodle.weight = 123;  // there is no such field in Dog class definition, but we still can set it automaically

function Dog() {
  this.email = 'dog@gmail.com';  // public instance variable
}
```
We also can add a method on the fly to that particular object, that has no definition in class:
```javascript
var poodle = new Dog();
poodle.bite = function() {
  console.log('I can bite!');
}

function Dog() {
  // no definition of 'bite' method
}
```
It is even possible to modify a functionality of method within a class on the fly:
```javascript
var poodle = new Dog();
poodle.bite = function() {   // method created on the fly
  console.log('I can bite!');
}
poodle.getName = function() { // change original behavior on the fly
  this.bite();
}

function Dog() {
  var name;
  this.getName = function() {  // original behavior
    return name;
  }
}
```
#### Prototype
Prototype is like a parent (object) to all objects created from a certain class. It is a place in the memory on the hip where all objects reside:
```javascript
Dog.prototype = new Object;
```
To set a property-value pair for all objects from prototype:
```javascript
function Dog () {
    var name;
}

var poodle = new Dog();
var beagle = new Beagle();

Dog.prototype = {'city':'madison'}; // Now all objects of class Dog will have the instance variable with value of 'madison'
console.log(poodle.city); // prints madison
console.log(beagle.city); // pirnts madison
```
When JavaScript trys to find an instance variable it looks inside the class definition. If cannot find it there it looks inside the prototype.

#### Inheritance
To create a parent for a class use prototype. Create a class that represents a parent class:
```javascript
Dog.prototype = new ParentDog();

function ParentDog() {
  var city;
  this.getCity() {
    return city;
  }
  this.setCity(value) {
    city = value;
  }
}
```
To change the property value set in prototype use its setters and getters:
```javascript
// Dog class
function Dog() { 
  var name;
  this.getName = function() {  // original behavior
    return name;
  }
}

// objects of class Dog
var poodel = new Dog();
var beagle = new Dog();

// parent class (prototype) to class Dog
function ParentDog() {
  var city; // use a private variable here
  this.getCity() {
    return city;
  }
  this.setCity(value) {
    city = value;
  }
}

// assign new property to all objects of class Dog
console.log(poodel.setCity('Verona');  // All objects from class Dog will have the same property now with the same value 'Verona'
```
If a public variable is set in prototype, when changed in the script dynamically, JavaScript will create a copy of that particlular object!

The use of prototype is helpful when you have a lot of objects to instantiate. If all objects will have similar functionality, define the functionality in prototype (parent) object and save a lot of memory.
