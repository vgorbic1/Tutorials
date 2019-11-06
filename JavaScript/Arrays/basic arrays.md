## Arrays
Arrays are variables that can hold more than one value. To initiate array:
```javascript
var cars = new Array();
```
or
```javascript
cars = Array();
```
To assign first pocket in the array:
```javascript
cars[0] = "Toyota";
```
To initiate the array and assign *Toyota* to the first pocket in the array:
```javascript
var cars = ["Toyota"];
```
To see content of array use F-12 and check console:
```javascript
console.log(nameOfArray);
```
To walk through an array use **for** loop and a ```length``` property:
```javascript
var cars = new Array("Toyota", "Ford");

for (i=0; i<cars.length; i++) {
    document.write(cars[i]);
}
```

#### Array methods
**concat()** method is used to combine the elements of two or more arrays and return a new array containing all of the elements.
```javascript
var fruits = new Array('oranges', 'apples');
var veggies = new Array('corn', 'peas');
var meats = new Array('fish', 'chicken')
var all = fruits.concat(veggies, meats);
```

**join()** method is used to combine the elements of an array into a single string, with each element separated by a character sent
as aparameter to the method. If no parameteer is sent, a comma is used as the default separator:
```javascript
var fruits = new Array('oranges', 'apples', 'pears');
var all = fruits.join();  / results in a string 'oranges,apples,pears'
var all = fruits.join(:);  / results in a string 'oranges:appels:pears'
```

**pop()** method is used to remove the last element from an array.
```javascript
var fruits = new Array('oranges', 'apples', 'pears');
fruits.pop();  // results in array that has 'oranges' and 'apples'
var removed = fruits.pop();  // 'remove' variable contains 'appples' in it
```

**push()** method is used to add elements to the end of an array. The parameters sent to the method are the new element or elements to add.
```javascript
var fruits = new Array('oranges', 'apples');
fruits.push('pears', 'grapes');  // adds pears and grapes to the array
```

**reverse()** method is used to reverse the order of the elements in an array.
```javascript
var fruits = new Array('oranges', 'apples', 'pears');
fruits.reverse();
```

**shift()** method is used to remove the first element of the array. It returns the value of the element that was removed.
```javascript
var fruits = new Array('oranges', 'apples', 'pears');
fruits.shift()  // now the array has only apples and pears
```

**unshift()** method is used to add elements to the beginning of an array.
```javascript
var fruits = new Array('apples', 'oranges');
fruits.unshift('pears', 'grapes');  // now the array has pears, grapes, apples and oranges
``` 

**slice()** method is used to slice a specified section of an array and then to create a new array using the elements from the sliced section of the old array.
```javascript
var fruits = new Array('oranges', 'apples', 'pears', 'grapes');
var someFruits = fruits.slice(1, 3);  // slice the second elemet (index number 1) through the third element (index number 2)
// or
var someFruits = fruits(2, 1, "watermelons");  // second element is removed, only one element removed, add 'watermelons' in place of the second element.
```

**sort()** method sorts an array in alphabetical order.
```javascript
var fruits = new Array('oranges', 'apples', 'pears');
fruits.sort();
```

