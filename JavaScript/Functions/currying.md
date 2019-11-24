## Currying
Currying means creating a partial parameter for a function.

### Currying with *bind()*
We can reuse one parameter to create functions that use it:
```js
function multiply(a, b) {
    return a * b;
}

var multipleByTwo = multiply.bind(this, 2);
console.log(multipleByTwo(4));

var multipleByThree = multiply.bind(this, 3);
console.log(multipleByThree(4));
```
