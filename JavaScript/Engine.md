## Engines

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

