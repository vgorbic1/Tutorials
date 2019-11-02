## Destructuring
The object and array literal expressions provide an easy way to create ad hoc packages of data:
```js
var x = [1, 2, 3, 4, 5];
```
The destructuring assignment uses similar syntax, but on the left-hand side of the assignment 
to define what values to unpack from the sourced variable:
```js
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```
### Defaults
A variable can be assigned a default, in the case that the value unpacked from the array is `undefined`.
```js
var a, b;

[a=5, b=7] = [1];
console.log(a); // 1
console.log(b); // 7
```
### Swapping variables
Without destructuring assignment, swapping two values requires a temporary variable:
```js
var a = 1;
var b = 3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1

var arr = [1,2,3];
[arr[2], arr[1]] = [arr[1], arr[2]];
console.log(arr); // [1,3,2]
```
### Parsing an array returned from a function
It's always been possible to return an array from a function. Destructuring can make
working with an array return value more concise.
```js
function f() {
  return [1, 2];
}

var a, b; 
[a, b] = f(); 
console.log(a); // 1
console.log(b); // 2
```
### Ignoring some returned values
You can ignore return values that you're not interested in:
```js
function f() {
  return [1, 2, 3];
}

var [a, , b] = f();
console.log(a); // 1
console.log(b); // 3
```
### Assigning the rest of an array to a variable
```js
var [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]
```
### Object destructuring
```js
var o = {p: 42, q: true};
var {p, q} = o;

console.log(p); // 42
console.log(q); // true
```
### Assigning to new variable names
```js
var o = {p: 42, q: true};
var {p: foo, q: bar} = o;
 
console.log(foo); // 42 
console.log(bar); // true
```
### Rest in Object Destructuring
```js
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40}
a; // 10 
b; // 20 
rest; // { c: 30, d: 40 }
```
