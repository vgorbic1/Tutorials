## Modules
Modules give us a better way to group variables and functions together.
In JavaScript we have the *Global Scope* and *Function Scope*. Later *Block Scope* was added. With an addition
of *Module Scope* we can groupe functions so they can use same variables form the *Global Scope*.

Scope Hierarchy:
- -Global Scope
- --Module Scope
- ---Function Scope
- ----Block Scope (const and let)

### The Module Pattern
This is how modules were written before ES Modules. This option uses IIFEs to create an internal scope. Thus, *Function scope* mimics *Block Scope*.
```js
(function() {
  // variables are not in Global Scope anymore:
  var harry = 'Potter'
  var voldemort = 'he who must not be named'
  
  function fight(opponent1, opponenet2) {
    var attack1 = Math.floor(Math.random() * opponent1.length);
    var attack2 = Math.floor(Math.random() * opponent2.length);
    return attack1 > attack2 ? `${opponent1} wins` : `${opponent2} wins`;
  }
  
  console.log(fight(harry, voldemort));
})();
```
Now, just name the IFFE and have access to the inner *fight()* function:
```js
// Global Scope
var ron = 'Ron';
var hagrid = 'Hagrid';

var fightModule = (function() {
  // variables are not in Global Scope:
  var harry = 'Potter'
  var voldemort = 'he who must not be named'
  
  function fight(opponent1, opponenet2) {
    var attack1 = Math.floor(Math.random() * opponent1.length);
    var attack2 = Math.floor(Math.random() * opponent2.length);
    return attack1 > attack2 ? `${opponent1} wins` : `${opponent2} wins`;
  }
  
  return {
    fight: fight
  }
})();

fightModule.fight(ron, hagrid);
```
And also you may use a global variable inside the module, but without modifying it in the *Global Scope*:
```js
// Global Scope
var ron = 'Ron';
var hagrid = 'Hagrid';

// Use global as a parameter
var fightModule = (function(ron) {
  // variables are not in Global Scope:
  var harry = 'Potter'
  var voldemort = 'he who must not be named'
  
  // Change global:
  ron = 'Hagrid';
  
  function fight(opponent1, opponenet2) {
    var attack1 = Math.floor(Math.random() * opponent1.length);
    var attack2 = Math.floor(Math.random() * opponent2.length);
    return attack1 > attack2 ? `${opponent1} wins` : `${opponent2} wins`;
  }
  
  return {
    fight: fight,
    ron: ron
  }
})(ron);

// Global is intact:
console.log(ron);

// Global is used in modal:
console.log(fightModule.ron);
```
But there are still two cons to this approach:
- Global Scope is still poluted and namespace clashes may occure.
- The order of scripts (if in several JS files) should allow for correct executing of entire code.
### CommonJS and AMD
CommonJS and AMD (Asyncronous Module Definition) provides no interference with *Gobal Scope*. CommonJS was created for use on servers (NodeJS). To bundle all modules (or separate files) in one, Browserify should be used. It is a command line tool that producess a bundle file from all dependent files or scripts, combining all modules.
```js
// --script.js--
var module1 = require(module1)
var module2 = require(module2)

function fight() {
 ...
}

module.exports = {
  fight: fight
}
```
```
> browserify script.js > bundel.js
```
AMD was designed specifically for browsers. It loads scripts or modules asyncronously.
```js
define(['module1', 'module2'],
  function(module1Import, module2Import) {
    var module1 = module1Import
    var module2 = module2Import
    
    function dance() {
      ...
    }
    
    return {
      dance: dance
    }
  }
);
```
### ES6 Modules
ES 6 Modules is a native JavaScript Solution to module implementation.
```js
import module1 from 'module1'
import module2 from 'module2'

export function jump() {
  
