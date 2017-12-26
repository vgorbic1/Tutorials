## Arrow Functions (Fat Arrow Functions)
An arrow function expression has a shorter syntax than a function expression and does not have its own 
*this*, arguments, *super*, or *new.target*. These function expressions are best suited for non-method functions, and they cannot 
be used as constructors.

### Basic Syntax:
```javascript
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
// equivalent to: (param1, param2, …, paramN) => { return expression; }

// Parentheses are optional when there's only one parameter name:
(singleParam) => { statements }
singleParam => { statements }
singleParam => expression

// The parameter list for a function with no parameters should be written with a pair of parentheses.
() => { statements }
```
### Examples:
Normal function expression:
```javascript
const sayHello = function() {
  console.log('Hello');
}
```
Same with arrow function:
```javascript
const sayHello = () => {
  console.log('Hello');
}
```
Since it is one line function, it does not need braces:
```javascript
const sayHello = () => console.log('Hello');
```

Normal function expression with a return:
```javascript
const sayHello = function() {
  return 'Hello';
}
```
Same with arrow function:
```javascript
const sayHello = () => 'Hello';
```

If an object literal is returned with a normal function:
```javascript
const sayHello = function() {
  return { msg: 'Hello' };
}
```
With arrow function use parenthesis:
```javascript
const sayHello = () => ({ msg: 'Hello' });
```

If a single parameter is used with notrmal function expression:
```javascript
const sayHello = function(name) {
 console.log(`Hello ${name}`);
}
```
With arrow function a single param does not need parenthesis
```javascript
const sayHello = name => console.log(`Hello ${name}`);
```

If multiple parameters are used with notrmal function expression:
```javascript
const sayHello = function(firstName, lastName) {
 console.log(`Hello ${firstName} ${lastName}`);
}
```
With arrow function, multuiple params need parenthesis:
```javascript
const sayHello = (firstName, lastName) => console.log(`Hello ${firstName} ${lastName}`);
```

### Another Example 
```javascript
const users = ['Nathan', 'John', 'William'];

const nameLengths = users.map(function(name) {
  return name.length;
});

// Shorter
const nameLengths = users.map((name) => {
  return name.length;
});

// Shortest
const nameLengths = users.map(name => name.length);

console.log(nameLengths);
```
