## Loops
Most popular are **while** and **for** loops. 

#### while loop
To create a **while** loop first assign an index (i) variable:
```javascript
var i = 0;
while (i < 5) {
  document.write("Hello!");
  i++;  // increment by one
}
```
Always use ```i++``` in the block of code.

#### do while loop
This loop will run at least one time.
```javascript
var i = 0;
do {
  document.write("Hello!");
} while (i<2);
```

#### for loop
To create a **for** loop:
```javascript
for (i=0; i<5; i++) {
  document.write("Hello!");
}
```
If you don't know the value of the tested variable (do not know when to stop the loop), use **while** loop. If you know the value of the tested variable (do know when to stop the loop), use **for** loop.

It is possible to inititate several variables as a statement:
```javascript
if (i=0, len=cars.length; i<len; i++) {
  ...
}
```
It is possible to omit a statement, if index variable set globally:
```javascript
var i = 0;
var len = cars.length;
if (; i<len; i++) {
  ...
}
```

#### break statement
Use break statement to jump from the loop. Usually used with a conditional statement:
```javascript
for (i=0; i<10; i++) {
  if (i == 3) break;
  document.write("Not three");
}
```

#### continue statement
Continue statement breaks one iteration in the loop and continues with the next one. In other words, it skips one iteration.
```javascript
for (i=0; i<10; i++) {
  if (i == 3) continue;
  document.write("Never three");
}
```

#### for in loop
To create **for in** loop:
```javascript
const user = {
  firstName: 'John', 
  lastName: 'Doe',
  age: 40
}

for(let x in user){
  console.log(`${x} : ${user[x]}`);
}
```
Everytime you go over the loop, the *x* becomes next element of the object *user*. Great for object properties iteration.

#### for each loop
To create **foreach** loop:
```javascript
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];

cars.forEach(function(car, index, array){
  console.log(`${index} : ${car}`);
  console.log(array);
});
```
Use an ananymous function with one or all three parameters. Great for array iteration.

#### map loop
To crete a **map** loop:
```javascript
const users  = [
 {id: 1, name:'John'},
 {id: 2, name: 'Sara'},
 {id: 3, name: 'Karen'},
 {id: 4, name: 'Steve'}
];

const ids = users.map(function(user){
  return user.id;
});
```
Use an ananymous function wtih a parameter as an object name. Great for arrays of objects iteration.
