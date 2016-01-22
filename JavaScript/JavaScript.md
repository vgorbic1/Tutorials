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
Most popular loops are **while** and **for** loops. To create a **while** loop first assign an index (*i*) variable:
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
If you don't know the value of the tested variable, use **while** loop. If you know the value of the tested variable,
use **for** loop.
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
