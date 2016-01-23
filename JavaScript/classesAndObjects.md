## Object Oriented Programming with JavaScript
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

var james = new Person("programmer", "no");
````
#### Creating a class
```javascript
function Dog(breed) {
    this.breed = breed;
}

var sparky = new Dog("poodle");
```
#### Adding Functions (Methods) to an object
Using **literal notation**:
```javascript
var Person = {
    age: age;
    birth_year: birth_year,
    year_now: function() {
        age + birth_year;
    }
};

var peter = new Person(10, 1975);  // create an object 
document.write(peter.year_now());  // use the function to calculate the year
```
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
