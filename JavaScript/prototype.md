## Prototype
Every JavaScript object has a prototype. The prototype is also an object. All JavaScript objects inherit their properties and methods from their prototype.

The Object.prototype is on the top of the prototype chain. All JavaScript objects (Date, Array, RegExp, Function, ....) inherit from the Object.prototype.

#### Creating a Prototype
The standard way to create an object prototype is to use an object constructor function:
```javascript
// The constructor function is the prototype for your person objects:
function person(first, last, age, eyecolor) {
    // public variables:
    this.firstName = first; 
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
```
`new` keyword creates new objects from the same prototype. 
```javascript
var myFather = new person("John", "Doe", 50, "blue");
var myMother = new person("Sally", "Rally", 48, "green");
```

#### Adding a Property to an Object
If you need to add new property to an existing object:
```javascript
myFather.nationality = "English";
```
The property will be added to `myFather`. Not to myMother. Not to any other person objects.

#### Adding a Method to an Object
If you want to add a new method to an existing object, use ananymous function:
```javascript
myFather.name = function () {
    return this.firstName + " " + this.lastName;
};
```
The method will be added to myFather. Not to myMother. Not to any other person objects.

#### Adding Properties to a Prototype
You cannot add a new property to a prototype the same way as you add a new property to an existing object, because the prototype is not an existing object. To add a new property to a constructor, you must add it to the constructor function:
```javascript
function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
    this.nationality = "English"; // Prototype properties can have prototype values (default values).
}
```

#### Adding Methods to a Prototype	
Your constructor function can also define methods:
```javascript
function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
    this.name = function() {
                    return this.firstName + " " + this.lastName;
                };
}
```

#### Adding Properties Using "prototype" Keyword
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

#### Adding Methods Using "prototype" Keyword
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
Only modify your own prototypes. Never modify the prototypes of standard JavaScript objects.
