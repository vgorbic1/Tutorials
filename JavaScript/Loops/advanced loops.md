## Advanced Loops

### forEach()
The **forEach()** method executes a provided function once for each array element.

To create **foreach** loop:
```js
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];

cars.forEach( 
  function (car, index, array) {
    console.log(`${index} : ${car}`);
    console.log(array);
  }
);
```
Use an ananymous function with one or all three parameters. Great for array iteration.

### forEach() ES6 syntax
Simplify forEach() loop with the ES6 *fat arrow* syntax:
```js
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];

cars.forEach( (car) => console.log(`${index} : ${car}`) );
```

### for ... of
The **for...of** statement creates a loop iterating over **iterable** objects. It invokes a custom iteration hook 
with statements to be executed for the value of each distinct property of the object.
```js
const array1 = ['a', 'b', 'c'];

for (const element of array1) {
  console.log(element);
}

// expected output: 
// "a"
   "b"
   "c"
```

### for ... in
The **for...in** statement iterates over all non-Symbol, **enumerable** properties of an object. 
Can be used with arrays, because arrays are objects.
```js
var obj = { a: 1, 
            b: 2, 
            c: 3 };
    
for (const prop in obj) {
  console.log(`${prop} = ${obj[prop]}`);
}

// Output:
// "a = 1"
// "b = 2"
// "c = 3"
```
[MORE](https://www.freecodecamp.org/news/the-complete-guide-to-loops-in-javascript-f5e242921d8c/)
