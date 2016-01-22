## Object Oriented Programming with JavaScript
### Objects
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
### Classes
#### Creating a class
```javascript
function Dog(breed) {
    this.breed = breed;
}

var sparky = new Dog("poodle");
```
