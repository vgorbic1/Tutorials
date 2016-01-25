## Loops
Most popular loops are **while** and **for** loops. 

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

#### for in loop
To create **for in** loop:
```javascript
for (var key in dogs) {
    console.log(key);
}
```
Everytime you go over the loop, the key becomes next property of the object *dogs*.
