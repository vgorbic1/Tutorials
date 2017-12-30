## Generators
 Generators provide a powerful alternative to iterators: they allow you to define an iterative algorithm 
 by writing a single function which can maintain its own state.

A GeneratorFunction is a special type of function that works as a factory for iterators. 
When it is executed it returns a new Generator object. A function becomes a GeneratorFunction 
if it uses the `function*` syntax.
```javascript
function* sayNames() {
  yield 'Jack';
  yield 'Jill';
  yield 'John';
}

const name = sayNames();

console.log(name.next().value);
console.log(name.next().value);
console.log(name.next().value);
```
Example:
```javascript
// ID Creator
function* createIds() {
  let index = 1;

  while(true) {
    yield index++;
  }
}

const gen = createIds();

console.log(gen.next().value);
console.log(gen.next().value);
console.log(gen.next().value);
```
