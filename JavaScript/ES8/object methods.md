## Object Methods
### Object.values()
The **Object.values()** method returns an array of a given object's values.
```js
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.values(object1));
// expected output: Array ["somestring", 42, false]
```
[MORE &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Object/values)

### Object.entries()
The **Object.entries()** method returns an array of a given object's own enumerable string-keyed property [key, value] pairs.
```js
const object1 = {
  a: 'somestring',
  b: 42
};

console.log(Object.entries(object1));

// expected output:
// console.log(Object.entries(object1));

for (let [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"
// order is not guaranteed
```
[MORE &rarr;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Object/entries)
