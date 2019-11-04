## Padding
The **padStart()** method pads the current string with another string (multiple times, if needed)
until the resulting string reaches the given length. The padding is applied from the start of the current string.
```js
'abc'.padStart(10);         // "       abc"
'abc'.padStart(10, "foo");  // "foofoofabc"
'abc'.padStart(6,"123465"); // "123abc"
'abc'.padStart(8, "0");     // "00000abc"
'abc'.padStart(1);          // "abc"
```
The **padEnd()** method pads the current string with a given string (repeated, if needed) 
so that the resulting string reaches a given length. The padding is applied from the end of the current string.
```js
'abc'.padEnd(10);          // "abc       "
'abc'.padEnd(10, "foo");   // "abcfoofoof"
'abc'.padEnd(6, "123456"); // "abc123"
'abc'.padEnd(1);           // "abc"
```
