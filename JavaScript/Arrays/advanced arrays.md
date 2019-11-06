## Advanced Arrays
If you need to loop through an array, most likely you deal with one of these three array methods:
- map
- filter
- reduce
### Map
The map() method **creates a new array** with the results of calling a provided function on every element in the calling array.
```js
const arr = [1, 2, 3, 4]; 
// multiply each element of the array by 2

// pass a function to map
const result = arr.map(x => x * 2);

console.log(result);
// expected output: Array [2, 4, 6, 8]
```
[MORE ON MAP &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
### Filter
The filter() method **creates a new array** with all elements that pass the test implemented by the provided function.
```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
// get only those words that are longer than 6 letters

// pass a function to filter
const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```
[MORE ON FILTER &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
### Reduce
The most powerful method. You can do even map() and filter() functionality with just reduce().

The reduce() method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.
```js
const arr = [1, 2, 3, 4];
// sum all elements in the array

// create reducer function
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// Add all elements of the array (1 + 2 + 3 + 4)
console.log(arr.reduce(reducer));
// expected output: 10

// Add all elements of the array, but start with 5 (5 + 1 + 2 + 3 + 4)
console.log(arr.reduce(reducer, 5));
// expected output: 15
```
[MORE ON REDUCE &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
