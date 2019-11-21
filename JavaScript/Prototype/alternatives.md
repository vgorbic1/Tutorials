## Alternative Ways to Create Objects and Prototypes
Use Object.create() function:
```javascript
const personPrototypes = {
  greeting: function() {
    return `Hello there ${this.firstName} ${this.lastName}`;
  },
  getsMarried: function(newLastName) {
    this.lastName = newLastName;
  }
}
```
Create an object using prototype above and extra properties:
```javascript
const mary = Object.create(personPrototypes);
mary.firstName = 'Mary';
mary.lastName = 'Williams';
mary.age = 30;

mary.getsMarried('Thompson');
console.log(mary.greeting());
````
### Alternative (shorter) way to do the same:
```javascript
const mary = Object.create(personPrototypes, {
  firstName: {value: 'Mary'},
  lastName: {value: 'Williams'},
  age: {value: 30}
});

mary.getsMarried('Thompson');
console.log(mary.greeting());
```
