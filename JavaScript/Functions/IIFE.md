## Immediately Invoked Function Expression (IIFE)
IIFE is a design pattern used buy many libiraries to avoid name space collision.
```js
(function() {
  ...
})()
```
Since the keyword *function* is inside round brackets, compiler understands it as
an expression, not a function declaration. Than we create an anonymous function 
and immediately invoke it, because you cannont call a function declaration right
away:
```js
function() {...}() // Error!
```

### Polute global name space only once
Now we can have a lot of variables within on functional space, and only one variable 
in global space:
```js
var script = (function() {
  var a = 10;
  var b = ' words';
  var c = function() {
    return a + b;
  }
  return {
    a: a,
    b: b,
    c: c()
  }
})();

console.log(script.a);
console.log(script.b);
console.log(script.c);
```
