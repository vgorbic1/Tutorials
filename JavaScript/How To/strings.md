### How To with Strings
Strings are objects within the JavaScript language. They are not stored as character arrays, 
so built-in functions must be used to manipulate their values. The functions provide various 
ways to access the contents of a string variable.

### Split a string
```js
onst originalString = "How are you?";
// Split string by whitespace character
const splitString = originalString.split(" ");
```
### Trim a whitespace
```js
const tooMuchWhitespace = "     How are you?     ";
const trimmed = tooMuchWhitespace.trim();
```
### Find and Replace String Values
```js
const originalString = "How are you?"
// Replace the first instance of "How" with "Where"
const newString = originalString.replace("How", "Where");
```
### Convert String To Number
```js
function stringToNumber(input) {
  return Number(input)
}
```
### Remove Last Character From String
```js
function removeLastCharacter(str){
  let charcter_arr = str.split('');
  return charcter_arr.slice(0, charcter_arr.length - 1).join('');
}
```
or
```js
function removeLastCharacter(str){
  return str.substring(0, str.length - 1);
}
```
