## *this* keyword and binding
*this* is the object that the function is a property of:
```
object.aFunction(this) // *this* refers to the object that the function is a property of
```

The keyword *this* is dynamically scoped, meaning that its scope is determied when it is called.

*this* usually refers to *window* object, unless another object calls it:
```js
const obj = {
  name: 'Billy',
  sing: function() {
    console.log(this) // in this case, it's a method on an object *obj*
    var anotherFunc = function() {
      console.log(this) // this points to *windows*, because the sing() function calls it!
    }
    anotherFunc()
  }
}

obj.sing()
```
### Binding with *new*
Used with a constructor function. Assign *this* to the object to be instanciated:
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const person = new Person('John', 25)
```
To fix that, use either *bind()*, a placeholder variable (that copies *this* that refers to the object), or an arrow function,
that always have a lexical scope.
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
