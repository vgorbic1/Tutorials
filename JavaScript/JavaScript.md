# JavaScript
## Fundamentals
JavaScript is a scripting language, mostly used on the client-side (browser). 

### Variables
JavaScript is dynamically typed language, meaning that a content of variable
may change from number to string and back. It is not possible in statically typed languages (Java).
To create (initiate) a variable use var and the variable name or just a variable name: 
```javascript
var name;  // the value of the variable is undefined. It is impossible to say what datatype it is.
```
To assign value to variable:
```javascript
name = "John";  // now, the datatype is string
```
If a variable is not declared (no "var" keyword), but is given a value, it is authomatically GLOBAL.
There are small numbter of datatypes:
- number
- string
- object
- function
To create a function variable:
```javascript
var myFunction = function() {
    alert('Hello!');
}
```
There are two ways to use this function:
```javascript
alert(myFunction); // function definition
alert(myFunction()); // function execution
```
GLOBAL variables are declared outside of functions.
LOCAL variables are declared within a function.

### Assignment operators
```javascript
y = 5
x = ++y  // result x = 6 and y = 6
x = y++  // result x = 5 and y = 6
x = --y  // result x = 4 and y = 4
x = y--  // result x = 5 and y = 4

x = 10 and y = 5
Operator  Example    Same as      Result
=         x = y                   x = 5
+=        x += y     x = x + y    x = 15
-=        x -= y     x = x - y    x = 5
*=        x *= y     x = x * y    x = 50
/=        x /= y     x = x / y    x = 2

Adding strings and numbers:
x = 5 + 5  // result 10
x = "5" + 5  // result 55
x = "Hello" + 5  // result Hello5

Adding (appending) strings:
text = "Hello ";
text += "World!";  // result "Hello World!"
```

### Functions
Functions are premade blocks of code:
```javascript
function name() {
  // do something ...
}
```
To call a function in HTML header:
```javascript
name();
```
To call a function in HTML body:
```javascript
<script>name();</script>
```

### Arrays
Arrays are variables that can hold more than one value. To initiate array:
```javascript
var cars = new Array();
```
or
```javascript
cars = Array();
```
To assign first pocket in the array:
```javascript
cars[0] = "Toyota";
```
To initiate the array and assign *Toyota* to the first pocket in the array:
```javascript
var cars = ["Toyota"];
```
To see content of array use F-12 and check console:
```javascript
console.log(nameOfArray);
```
To walk through an array use **for** loop and a ```length``` property:
```javascript
var cars = new Array("Toyota", "Ford");

for (i=0; i<cars.length; i++) {
    document.write(cars[i]);
}
```

### Conditionals
Make sure **else if** are spelled separately. Not like in PHP!
```javascript
if (i === 5) {
  do something...
} else if (i === 2) {
  do something...
} else {
  do something...
}
```
Conditional operator:
```javascript
var voteable = (age < 18) ? "yes" : "no";
```
