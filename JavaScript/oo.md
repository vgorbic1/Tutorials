## Object Oriented Programming with JavaScript
JavaScript is a functional language, but it is possible to implement some features of object-oriented paradigm.

#### Creating a class
To create a class, just use a function keyword and the name the function with a capital letter.
```javascript
function Dog() {
}
```
Create a class with a pirvate "instance" variable. To make the instance private, use var keyword. To access this variable we need a public getter and setter:
```javascript
function Dog() {
  var name;

  this.getName = function() {
    return name;
  }
  
  this.setName = function(value) {
    name = value;
  }
}

var poodle = new Dog(); // Constructor to create an object "Poodle"
poodle.setName('Sparky');
console.log(poodle.getName());
```
To create a class with a public variable, just add a keyword this to it:
```javascript
function Dog() {
  this.name = "Sparky";
}

var poodle = new Dog();
console.log(poodle.name);
```
It is possible to pass a parameter to the class:
```javascript
function Dog(breed) {
    this.breed = 'breed';
}

var sparky = new Dog('poodle');
```

#### Creating objects
To create an object, one can use **literal notation**:
```javascript
var james = {
    name: "James",
    phone: "456-2345"
};
```
or **constructor notation**, to create a template for multiple objects (in other words, creating a class):
```javascript
function Person(job, married) {
    this.job = job;
    this.married = married;
};

var james = new Person("programmer", "no");  // Constructor to create an object
````

#### Adding functions (Methods) to an object
Using **constructor notation**:
```javascript
function Person(age, birth_year) {
    this.age = age;
    this.birth_year = birth_year,
    this.year_now = function() {
        this.age + this.birth_year;
    };
};

var peter = new Person(10, 1975);  // create an object 
document.write(peter.year_now());  // use the function to calculate the year
```
#### Getting value of an object
Using **dot notation**:
```javascript
myObject.nameProperty;
```
Using **bracket notation**, which has an advantage, since we can use another variable, not just a string:
```javascript
myObject["nameProperty"];

var myObject = {nameProperty: someValue};
var myProperty = "nameProperty";
myObject[myProperty];
```

#### Methods included into every object
To chek if an object has a particular property and if yes, return true use ```hasOwnProperty()```:
```javascript
var myObject = {name: "John", age: "39"};
console.log(myObject.hasOwnProperty("name");  // returns true
console.log(myObject.hasOwnProperty("year");  // returns false
```
To figure out the type of the variable (string, number, function, or object), use ```typeof``` operator:
```javascript
console.log(typeof myVariable);
```
To print all names/values of properties of an object use **for in** loop:
```javascript
var nyc = {
    fullName: "New York City",
    mayor: "Whoever",
    population: 8000000};
    
for (var key in nyc) {
    console.log(key);  // get properties' names
}

for (var key in nyc) {
    console.log(nyc[key]);  // get properties' values
}
```

#### Prototype
Every JavaScript object has a prototype. The prototype is also an object. All JavaScript objects inherit their properties and methods from their prototype. The `Object.prototype` is on the top of the prototype chain. All JavaScript objects (Date, Array, RegExp, Function, ....) inherit from the `Object.prototype`.

The JavaScript prototype property allows you to add new properties to an existing prototype:
```javascript
function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
person.prototype.nationality = "English";
```
The JavaScript prototype property also allows you to add new methods to an existing prototype:
```javascript
function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
person.prototype.name = function() {
    return this.firstName + " " + this.lastName;
};
```
