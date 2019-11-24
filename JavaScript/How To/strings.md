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
