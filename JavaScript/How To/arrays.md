### Flatten an Array
Use **flat()** method on the array. You can set a depth level specifying how 
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

### Turn an array into an object
The **Object.fromEntries()** method transforms a list of key-value pairs into an object.
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
### Remove all elements that property age is greater than 10
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
### How To Sort Array Of Objects
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
### How To Empty An Array
```js
let fruits = ["Orange", "Apple", "Pineapple"];
fruits.length = 0;
```
or
```js
let fruits = ["Orange", "Apple", "Pineapple"];
fruits = [];
```
