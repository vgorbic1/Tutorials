## Function and Block Scopes

**Function scope** is created with the keyword *function*:
```js
function a() {
  ...
}
```
**Block scope** is created with a set of curly brackets, so the function scope is a block scope too:
```js
for (i = 0; i < 10; i++) {
 ...
}
```
or 
```js
if (i < 10) {
  ...
}
```

### *var*
var keyword creates a functionally scoped variables. It means they are 
only available inside the function they’re created in, or if not created inside a 
function, they are **globally scoped**.

function scope:
```js
var a = 'a'
function fa() {
  var a = 'b';
}
fa();
console.log(a) // result a
```
block scope:
```js
var a = 'a'
if (true) {
  var a = 'b';
}
console.log(a) // result b (we mutated the variable in within the block)
```
### *const* and *let*
const and *let* create a block scoped variables.

function scope:
```js
let a = 'a'
function fa() {
  let a = 'b';
}
fa(); 
console.log(a); // result a
```
block scope:
```js
let a = 'a'
if (true) {
  let a = 'b';
}
console.log(a) // result a (no mutation in block scope)
```
