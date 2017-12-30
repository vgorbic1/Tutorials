## Iterators
An object is an iterator when it knows how to access items from a collection one at a time, 
while keeping track of its current position within that sequence. In JavaScript an iterator is an object that provides
a next() method which returns the next item in the sequence. 
This method returns an object with two properties: done and value.
```javascript
function nameIterator(names) {
  let nextIndex = 0;
  return {
    next: function() {
      return nextIndex < names.length ?
      { value: names[nextIndex++], done: false } :
      { done: true }
    }
  }
}
```
Example:
```javascript
// Create an array of names
const namesArr = ['Jack', 'Jill', 'John'];
// Initialize iterator (code above) and pass in the names array
const names = nameIterator(namesArr);

console.log(names.next().value);
console.log(names.next().value);
console.log(names.next().value);
```
