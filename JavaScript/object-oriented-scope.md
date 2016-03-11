## Classes with Instance Variables of Different Scope
Instance variables for classes could be of private or public scope.

#### Class with Public Instance Variables
```javascript
function Student() {
  this.name;
  this.email;
}

var StudentOne = new Student();

StudentOne.name = 'John';
StudentOne.email = 'johnn@example.com';

console.log(StudentOne.name + ' ' + StudentOne.email);  
```

#### Class with Private Instance Variables
To get access to the private instance variable you need to create accessors (getters) and mutators (setters):
```javascript
function Student() {
  var name;
  var email;
  // getters and setters
  this.getName = function() {
    return name;
  }
  this.setName = function(value) {
    name = value;
  }
  this.getEmail = function() {
    return email;
  }
  this.setEmail = function(value) {
    email = value;
  }
}

var studentOne = new Student;

studentOne.setName('John'); 
studentOne.setEmail('john@example.com');

console.log(studentOne.getName());
console.log(studentOne.getEmail());
```
Add another function to this class using `prototype` keyword:
```javascript
Student.prototype.register = function(name, course) {
                                 console.log(name + ' is registered for ' + course);
                             }
                             
var studentTwo = new Student();

studentTwo.register('Jim', 'JavaScript');                            
```
