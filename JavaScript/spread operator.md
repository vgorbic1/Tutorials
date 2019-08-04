## Spread Operator
Spreads an array or object into parameters to be used in functions
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
