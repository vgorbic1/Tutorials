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
JSON works with 'key:value' pairs, separated by comma.
If a collection of sutdent objects has an `id` as a property, it will look like this:
```javascript
[
  {'id':1},
  {'id':2},
  ['id':3}
]
```
Keys are typically strings, and have to be placed in quotes. If we have several properties, separate them with a comma too:
```javascript
[
  {'id':1, 'name':'Peter'},
  {'id':2, 'name':'John'},
  ['id':3, 'name':'James'}
]
```
We can have an object(s) included into anothe object:
```javascript
[
  {'id':1, 'name':'Peter', 'courses':[{}, {}, {}]},
  {'id':2, 'name':'John'},
  ['id':3, 'name':'James'}
]
```
#### Using JSON
To loop through all objects in a collection and get vslues of their properties:
```javascript
var courses = [{'title':'asp'}, {'title':'php'}, {'title':'java'}];

for (var i = 0; i < courses.length; i++) {
    console.log(courses[i].title);
}
```
To add functions:
```javascript
var courses = [
               {'title':'asp',
                'printDetails':function() {
                                   alert(this.title);
                               }
               }, 
               {'title':'php',
                'printDetails':function() {
                                   alert(this.title);
                               }
               },
               {'title':'java',
                'printDetails':function() {
                                   alert(this.title);
                               }
               }
              ];

for (var i = 0; i < courses.length; i++) {
    console.log(courses[i].title);
    courses[i].printDetails();
}
```
