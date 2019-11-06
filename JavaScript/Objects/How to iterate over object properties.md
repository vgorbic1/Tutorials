## How to iterate over object properties
### Object.keys() to get as strings
```js
const obj = {
  a: 'somestring',
  b: 42
};

Object.keys(obj).forEach((key, index) => {
  console.log(index, key, obj[key]);
});

// expected output
// 0 "a" "somestring"
// 1 "b" 42
```
### Object.entries() to get as arrays
```js
const obj = {
  a: 'somestring',
  b: 42
};

Object.entries(obj).forEach((prop, index) => {
  console.log(index, prop);
});

// expected output
// 0 ["a", "somestring"]
// 1 ["b", 42]
```
### Object.values() to get only value strings
```js
const obj = {
  a: 'somestring',
  b: 42
};

Object.values(obj).forEach((value) => {
  console.log(value);
});

// expected output
// "somestring"
// 42
```
