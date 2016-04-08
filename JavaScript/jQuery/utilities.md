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
*Merges two arrays, but uses a copy, so the original isn't altered.*

