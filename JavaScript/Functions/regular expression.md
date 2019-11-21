## Regular Expression Functions
#### match()
If there is a match it returns the result description in array or null if no match:
```javascript
let re = /hello/;
const str = 'Hello there';
const result = str.match(re);
console.log(result);
```
#### exac()
If there is a match it returns the result description in array or null if no match:
```javascript
let re = /hello/;
const result = re.exec('hello world');
console.log(result);
```
#### test()
If there is a match it returns true, false otherwise:
```javascript
let re = /hello/;
const result = re.test('Hello');
console.log(result);

// to make a case insensitive:
let re = /hello/i;
...
```
#### search()
Returns the index of the first match, -1 if not found:
```javascript
let re = /hello/;
const str = 'Hello there';
const result = str.search(re);
console.log(result);
```
#### replace()
Returns new string with some or all matches of a pattern
```javascript
let re = /hello/;
const str = 'Hello there';
const newStr = str.replace(re, 'Hi');
console.log(newStr);
```
