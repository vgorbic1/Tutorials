## jQuery Utilities

#### Merge Two Arrays
The `$.merge()` operation forms an array that contains all elements from the two arrays:
```javascript
var AFCteams = ["chiefs", "browns", "jets"];
var NFCteams = ["packers", "bears", "cowboys"];
	
var nfl = [];
$.merge(nfl, NFCteams);
$.merge(nfl, AFCteams);

// Result:
// ["chiefs", "browns", "jets"]
// ["packers", "bears", "cowboys", "chiefs", "browns", "jets"]
```
**Merges two arrays, but uses a copy, so the original isn't altered.**
```javascript
var first = [ "a", "b", "c" ];
var second = [ "d", "e", "f" ];
$.merge( $.merge( [], first ), second );
console.log(AFCteams);
console.log(nfl);

// Result:
// [ "a", "b", "c", "d", "e", "f" ]
```
[more here](https://api.jquery.com/jquery.merge/)

#### Merge Two Objects
The `$.extend()` operation merges the contents of two or more objects together into the first object.
```javascript
var defaults =  { "stories" : 1, "color" : "white", "garage" : "2 car garage" }
var userPreferences = { "color": "gray", "garage" : "3 car garage" }
var extendedObject = {};

$.extend(extendedObject, defaults, userPreferences);
console.log(extendedObject);
// Result: {stories: 1, color: "gray", garage: "3 car garage"}
	
$.extend(defaults, userPreferences);
console.log(defaults);
// Result: {stories: 1, color: "gray", garage: "3 car garage"}
```
[more here](https://api.jquery.com/jquery.extend/)

#### Iteration
The `$.each()` operator is generic iterator function, which can be used to seamlessly iterate over both objects and arrays. The `$.each()` function is not the same as `$(selector).each()`, which is used to iterate, exclusively, over a jQuery object. The `$.each()` function can be used to iterate over any collection, whether it is an object or an array.
```javascript
$.each([ 52, 97 ], function( index, value ) {
  alert( index + ": " + value );
});
// Result:
0: 52 
1: 97
```
Note, that `$.each()` function internally retrieves and uses the length property of the passed collection. So, if the collection has a property called length — e.g. `{bar: 'foo', length: 10}` — the function might not work as expected.
```javascript
var obj = {
  "flammable": "inflammable",
  "duh": "no duh"
};
$.each( obj, function( key, value ) {
  alert( key + ": " + value );
});

//Result:
flammable: inflammable 
duh: no duh
```
