## JSON
JavaScript Object Notation. JSON is the easiest format to work with data in JavaScript. There is only one type of collections in JavaScript - an array. 

#### Collection
The square brackets represent the collection:
```javascript
students = [];
```
In XML:
```xml
<students>
  <student></student>
  <student></student>
  <student></student>
  <student></student>
</students>
```
In JSON the root node is replaced with a square bracket:
```javascript
[
  <student></student>
  <student></student>
  <student></student>
  <student></student>
]
```

#### Object
In JavaScript an object is defined with curly brackets:
```javascript
student = {};
```
Collection of objecs in JSON will look like:
```javascript
[ 
  {}, {}, {}, 
]
```

#### Syntax
JSON workd with 'key:value' pairs, separated by comma.
If a collection of sutdent objects has an `id` as a property, it will look like this:
```javascript
[
  {'id':1},
  {'id':2},
  ['id':3}
]
```
Keys are typically strings, and have to be placed in quotes.
