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
#### Adding functions (Methods) to an object
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
