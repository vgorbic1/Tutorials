# JavaScript
## Fundamentals
JavaScript is a scripting language, mostly used on the client-side (browser).

###Document Object Model (DOM)
DOM is a convention for representing objects in HTML document.
### Variables
To create (initiate) a variable use var and the variable name or just a variable name: 
```javascript
var name;
```
To assign value to variable:
```javascript
name = "John";
```
If a variable is not declared, but is given a value, it is authomatically GLOBAL.

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

### Loops
Most popular loops are **while** and **for** loops. To create a **while** loop first assign an index *(i)* variable:
```javascript
var i = 0;
while (i < 5) {
  document.write("Hello!");
  i++;  // increment by one
}
```
To create a **for** loop:
```javascript
for (i=0; i<5; i++) {
  document.write("Hello!");
}
```
If you don't know the value of the tested variable (do not know when to stop the loop), use **while** loop. If you know the value of the tested variable (do know when to stop the loop), use **for** loop.

It is possible to inititate several variables as a statement:
```javascript
if (i=0, len=cars.length; i<len; i++) {
  ...
}
```
It is possible to omit a statement, if index variable set globally:
```javascript
var i = 0;
var len = cars.length;
if (; i<len; i++) {
  ...
}
```
To create **for in** loop:
```javascript
for (var key in dogs) {
    console.log(key);
}
```
Everytime you go over the loop, the key becomes next property of the object *dogs*.


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
