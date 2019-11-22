## Function Invocation
(invocation or calling or execution)

### Function Declaration
```js
function india() {
  console.log('warm')
}
```
This function is defined at compile time, when global execution context is
created and hoisting is in progress.

### Function Expression
```js
var russia = function() {
  console.log('cold')
}
```
This function is defined at *runtime*, when we run/invoce/call/execute
the function, before it *russia* is just a variable with *undefined* value.

### After Invocation
After a function got invoked (called, executed), a function execution context is created with:
- *this* keyword
- *arguments* keyword
- Variable Environment

#### *Arguments*
The *arguments* keyword gives access to the arguments of the executed function:
```js
function marry(person1, person2) {
  console.log(argumnents); // { 0: 'Tim', 1: 'Tina' }
  return `${person1} is married to ${person2}`; 
}
marry('Tim', 'Tina')
```
It gives an object with a key as an index and values of passed arguments.
To get arguments as an array use:
```js
console.log(Array.from(arguments)) // ['Tim', 'Tina']
```
or use a speread operator:
```js
unction marry(...args) {
  console.log(args); // ['Tim', 'Tina']
  ...
```
