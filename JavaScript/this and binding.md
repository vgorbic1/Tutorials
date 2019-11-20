## *this* keyword and binding
The keyword *this* is dynamically scoped, meaning that its scope is determied when it is called.
### New Binding
Used with a constructor function. Assign *this* to the object to be instanciated:
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const person = new Person('John', 25)
```

### Implicit binding
Here *this* keyword is applied to the ogject:
```js
const person = {
  name: 'John',
  age: 25,
  greet() {
    console.log('Hi, ' + this.name);
  }
}
```

### Explisit bindig
State exactly what *this* keyword should say:
```js
const person = {
  name: 'John',
  age: 25,
  timeOut: function() {
    this.setTimeout;
  }.bind(window);
}
``` 
Here *this* binds to the window object, instead of the person object.

### Arrow Functions
In arrow function a scope is always lexical, meaning wherether you write the function that it is scoped to:
```js
const person = {
  name: 'Karen',
  age: 40,
  hi: function() {
    var inner = () => {
      console.log('hi ' + this.name)
    }
    return inner()
  }
  bye: function() {
    var inner = function () {
      console.log(this.setTimeout)
    }
  }
}

person.hi() // 'this' refers to the object person
person.bye() // 'this' refers to the window object
```
