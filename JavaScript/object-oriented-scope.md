## Classes with Instance Variables of Different Scope
Instance variables for classes could be of private or public scope.
#### Class with a Provate Instance Variables
To get access to the private instance variable you need to create accessors (getters) and mutators (setters):
```javascript
function Student () {
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
```
