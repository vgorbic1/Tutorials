### Flatten an array
Use *flat()* method on the array. You can set a depth level specifying how 
deep a nested array structure should be flattened. Defaults to 1.
```js
var arr1 = [1, 2, [3, 4]];
arr1.flat(); 
// [1, 2, 3, 4]

var arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

var arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

var arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
[MORE &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

Use *reduce()* method:
```js
const data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];

const flat = data.reduce((total, amount) => {
  return total.concat(amount);
}, []);

flat // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```
### Turn an array into an object
The *Object.fromEntries()* method transforms a list of key-value pairs into an object.
```js
const entries = [
  ['foo', 'bar'],
  ['baz', 42]
];

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```
[MORE &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries)

### Extract sections of an array
*slice()* returns a new array containing the extracted elements.
```js
var fruits = new Array( "apple", "pear", "orange", "banana" );
alert ( fruits.slice ( 1, 3 ) )  // Displays "pear,orange"
alert ( fruits.slice ( 0, -2 ) ) // Displays "apple,pear"
alert ( fruits.slice ( 2 ) )     // Displays "orange,banana"
```
### Join arrays together
```js
var yellowFruits = new Array( "banana", "lemon" );
var orangeFruits = new Array( "orange", "mandarin" );
var orangeAndYellowFruits = yellowFruits.concat( orangeFruits );
var orangeYellowAndRedFruits = orangeAndYellowFruits.concat( "strawberry", "raspberry" );
```
### Convert an array to a string
```js
var fruits = [ "apple", "pear", "orange", "banana" ];
alert ( fruits.toString( ) ) ;  // displays "apple,pear,orange,banana"
alert ( fruits.join( ) ) ;      // displays "apple,pear,orange,banana"
alert ( fruits.join( "-" ) ) ;  // displays "apple-pear-orange-banana"
alert ( fruits.join( ", " ) ) ; // displays "apple, pear, orange, banana"
```
### Add and remove element(s) in the middle of an array
```js
var fruits = [ "apple", "pear", "orange", "banana" ];
var removedElements = fruits.splice ( 1, 2 );
alert ( fruits );  // displays "apple,banana"
alert ( removedElements );  // displays "pear,orange"

var fruits = [ "apple", "pear", "orange", "banana" ];
var removedElements = fruits.splice ( 2, 0, "cherry" );
alert ( fruits );  // displays "apple,pear,cherry,orange,banana"
alert ( removedElements );  // displays ""

var fruits = [ "apple", "pear", "orange", "banana" ];
var removedElements = fruits.splice ( 1, 2, "cherry" );
alert ( fruits );  // displays "apple,cherry,banana"
alert ( removedElements );  // displays "pear,orange"
```
### Create a new array where each element is slightly altered
use *map()* array function:
```js
let employees = [
    { "first_name": "Hari", "last_name": "Krishnan" },
    { "first_name": "Samuel", "last_name": "Jackson" },
    { "first_name": "Suriel", "last_name": "Johnson" },
    { "first_name": "Roy", "last_name": "Agasthyan" }
];

let full = employees.map(function(emp) {
    return emp["first_name"] + ' ' + emp["last_name"]
});

console.log(full) //  [ 'Hari Krishnan', 'Samuel Jackson', 'Suriel Johnson', 'Roy Agasthyan' ]
```
### Remove all elements where a property satisfies a certain criterion
Use *filter()* array function:
```js
let students = [
    { "first_name": "Hari", "age": 13 },
    { "first_name": "Suriel", "age": 12 },
    { "first_name": "Roy", "last_name": 10 }
];

// es5
var filtered_students = students.filter(function(student){
    return student.age > 10
});

// es6
let filtered_students = students.filter(student => student.age > 10);

console.log(filtered_students);

/* Output
[ { first_name: 'Hari', age: 13 }, { first_name: 'Suriel', age: 12 }]
```
### Sort array of objects
```js
let arr = [
  {'name' : 'Roy'},
  {'name' : 'James'},
  {'name' : 'Andrew'}
];

let sorted = sortData(arr, 'desc');
console.log(sorted)

function sortData(data, order = 'asc'){
  if(order == 'asc'){
    return data.sort((a,b)=>{ 
      if(a.name < b.name) return -1; // a comes first
      if(a.name > b.name) return 1; // b comes first
      return 0;
    });
  } else {
    return data.sort((a,b)=>{ 
      if(a.name < b.name) return 1; // b comes first
      if(a.name > b.name) return -1; // a comes first
      return 0;
    });
  }
  return data;
}
```
### Empty an array
```js
let fruits = ["Orange", "Apple", "Pineapple"];
fruits.length = 0;
```
or
```js
let fruits = ["Orange", "Apple", "Pineapple"];
fruits = [];
```
### Find duplicate values in an array
```js
// Find duplicates using for loop
let item_list = [1,2,3,4,5,5,5,7,8,2,3,4,4,4,4,4];

let duplicate = item_list.reduce((acc, currentValue, index, array) => {
  if (array.indexOf(currentValue) != index && !acc.includes(currentValue)) acc.push(currentValue);
  return acc;
}, []);

console.log('Duplicate items are ' + duplicate.join(','));
```
### Find a sum of array elements
Use *reduce()* for it:
```js
const euros = [29.76, 41.85, 46.5];
const sum = euros.reduce((total, amount) => total + amount);
```
### Find an average of all elements in an array
Use *reduce()* for it:
```js
const euros = [29.76, 41.85, 46.5];
const average = euros.reduce((total, amount, index, array) => {
  total += amount;
  if( index === array.length-1) { 
    return total/array.length;
  }else { 
    return total;
  }
});
```
### Map and filter an array in one loop
Use *reduce()* for it:
```js
const euro = [29.76, 41.85, 46.5];
const above30 = euro.reduce((total, amount) => {
  if (amount > 30) {
    total.push(amount);
  }
  return total;
}, []);

above30 // [ 41.85, 46.5 ]
```
### Create a tally from an array of things
Use *reduce()* to map eache element to number of its repeats in an the array:
```js
const fruitBasket = ['banana', 'cherry', 'orange', 'apple', 'cherry', 'orange', 
                      'apple', 'banana', 'cherry', 'orange', 'fig' ];
const count = fruitBasket.reduce( (tally, fruit) => {
  tally[fruit] = (tally[fruit] || 0) + 1 ;
  return tally;
} , {})

count // { banana: 2, cherry: 3, orange: 3, apple: 2, fig: 1 }
```
### Pipe several functions in one order using array
A pipeline is a term used for a list of functions that transform some initial 
value into a final value:
```js
function increment(input) { return input + 1;}
function decrement(input) { return input — 1; }
function double(input) { return input * 2; }
function halve(input) { return input / 2; }

let pipeline = [increment, double, decrement];
```
To find the total use *reduce()*. Instead of reducing an array of values we 
reduce over our pipeline of functions. This works because we set the initial 
value as the amount we want to transform:
```js
const result = pipeline.reduce(function(total, func) {
  return func(total);
}, 1);

result // 3
```
