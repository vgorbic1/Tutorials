## Engine

JavaScript Code &rarr; JavaScript Engine &rarr; CPU

[List of JavaScript Engines](https://en.wikipedia.org/wiki/List_of_ECMAScript_engines)

Most Notable:
- v8 Engine - Google Chrome, Node
- SpiderMonkey - Mozilla Firefox
- Chakra - Microsoft Edge
- JavaScriptCore - Apple Safari

### Interpreter vs Compiler
- Interpreter analyses given code on the fly line by line. Fast to get up
and running. Cannot optimize the code.
- Compiler works ahead of time, creates the full program out of the code
and returns a compiled version (Machine Code) to run by the machine. 
Compiler takes longer to get up and running, but can optimize code (loops and
other iterations)
- JIT Compiler (Just in time). Best of bboth worlds.

### Inside the Engine (V8) Process order:
- A JavaScript file is given

**Parser Phase**
- Engine perform Lexical Analysis creating tokens out of the script
- Tokens are formed in Abstract Syntax Tree (AST)

**Interpreter Phase**
- Creates a Bytecode out of AST (Ignition)
- Profiler analyses code and suggests optimizations
- If code may be optimized, the profiler sends code to compiler
**Compiler Phase** 

- Compiler (Turbofan) optimizes code (loops and repeats)
- Replaces sections where Bytecode may be improved with Machine Code

### Call Stack and Memory Heap
- Call Stack is needed to keep track of where we are in the code, so e can run the code in order.
- Memory Heap is a place to write into and store information. So we can alocate memory, use memory
and release memory

#### To create Stack Overflow
Use a recursion:
```js
function overflowIt() {
  overflowIt();
}

overflowIt();
```

#### To create Memory Leak
```js
let array = [];
for (let i = 1; i > 0; i++) {
  array.push[i];
}
```
Avoid this potential Memory Leaks:
- Global variables
- Event listeners

### Execution Context
When code is run on the JavaScript engine, a **Global execution context** is creted.
It is given by JavaScript event if the script file is empty. The Global context 
provides access to the Global Object (in a browser it is *Window* object) and to
the *this* keyword, which is a shortcut to the Global Object.

This is the order of a script compilation:
- Creating a Global execution context with the Global object and *this* keyword
- Hoisting (variables partially hoisted and function declarations are fully hoisted)
- Code runnning phase

When you run a function a new **Funnction execution context** is created.

### Lexical Environment
(Same as Lexical Scope or Lexical Analysis) this is where you write something. Everytime 
an **Execution context**, a new Lexical Environment is also created for that scope.
```js
function funcOne() { // this one is lexical (written) to  the Global context
  const a = 1
  return a
}

function funcTwo() { // this one is lexical (written) to  the Global context

  function insider() { // this one is lexical to the funcTwo execution context
    const b = 5
    return b
  }
  
  let c = insider();
  return c + 5
}
```
### Hoisting
During the initial pass through the code, the compiler allocates memory for some variables and all 
functions during the global scope creation phase and before executing phase.
- Variables defined with a keyword *var* are partially hoisted, because they are given `undefined` value,
before a value is assigned later in the code.
- Functions (defined with a keyword *functionn* are fully hoisted, because a function declaraiton is assigned a memory
space right away. Function expression is not hoisted!
```js
console.log(sing1()); // "la-la" (function is fully hoisted
console.log(sing2); // undefined (variable is partially hoisted)
console.log(sinng2()); // Error (nothing to run, the variable is undefined!)

funciton sing1() { // function declaration
  console.log('la-la');
}

var sing2 = function () { // function expression
  console.log('la-la');
}
```
