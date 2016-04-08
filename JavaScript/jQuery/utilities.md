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
