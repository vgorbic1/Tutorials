### How To Split Number To Individual Digits
```js
function splitToDigit(n){
  return [...n + ''].map(Number)
}

console.log(splitToDigit(100))
```
