## Closures
Closures is one of two pillars of JavaScript (along with Prototypes).
1. In JavaScript one can pass functions around as any other data.
2. Lexical Scope - the JavaScript engine knows (based on where our code is written) before we even run the code, 
what variables each function has acces to.
Closure is just a combination of a function and Lexical Environment.

### Closure Example
```js
function a() {
  let father = 'Father'
  return function b() {
    let son = 'Son'
    return function c() {
      let holySpirit = 'Holy Spirit'
      return `${father}, ${son}, and ${holySpirit}`
    }
  }
}

a()()() // returns 'Father, Son, and Holy Spirit'
```
Here even when function a() is popped from the stack, variable father is still in memory in a special `Closure` box 
on the heap! It is not garbage-collected. It is still available for function b() and function c(). Same goes with variable son. 
This is what closure means.

### Another Closure Example
```js
const boo = (name) => (name2) => (name3) => console.log(`${name} ${name2} {$name3}`)
boo('Peter')('John')('James') // prints 'Peter John James'

const stringBoo = boo('one')('two')('three')

// call the function later in the script and it still has the values accessible in memory:
stringBoo();
```

### JavaScript API Cloures Example
Many JavaScript Web API functions have closure functionality:
```js
function callMeMaybe() {
  const name = 'Margaret'
  setTimeout(function() {
    console.log(name)
  }, 4000);
}

callMeMaybe();
```

### Benefits of Closures
- Closures are memory efficient
```js
// Not memory efficient way, each time a new array is created and destroyed after:
function heavyDuty(i) {
  const arr = new Array(10000).fill("hi")
  return arr[i]
}

heavyDuty(256);
heavyDuty(1298);
heavyDuty(7236);

// Solution with closures. Array is created only once:
function heavyDuty() {
  const arr = new Array(10000).fill("hi")
  return function(i) {
    return arr[i]
  }
}

const getHeavyDuty = heavyDuty();

getHeavyDuty(256);
getHeavyDuty(1298);
getHeavyDuty(7236);
```


