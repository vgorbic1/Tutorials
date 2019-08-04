## Spread Operator
Spreads an array or object into variables
### Object Spread Operator
```js
const animals = {
  lion: 23,
  monkey: 3,
  tiger: 12
}

// now crate a new variables:
const {lion, ...rest} = animals
console.log(tiger) // gives 12
console.log(rest) // gives {lion: 23, monkey: 3}
```
### Array Spread Operator
```js
const array = [1,2,3,4,5]

function sum(a, b, c, d, e) {
  return a + b + c + d + e
}

sum(...array);
```
