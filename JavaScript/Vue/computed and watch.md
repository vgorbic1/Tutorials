## Computed Object
The Vue native `computed` object allows for caching the value of a variable that may be changed during runtime.
In the function, you may set up the logic how this variable should be computed. Use variables in `computed` more
often, because they are more efficient. `Computed` variables are working only with syncronous tasks. For unsync tasks
use `watch` object.
```javascript
...
data: {
  counter: 0
},
computed: {
  output: function() {
    return this.counter > 5 ? 'Greater than 5' : 'Smaller than 5';
  }
}
...
```
 
## Watch Object
the `watch` is doing similar task, but all the way around. It takes a declared in `data` variable and watches if it is changed.
If it is changed, a certain method is triggered. This allows to react to changes.
```javascript
...
data: {
  counter: 0
},
watch: {
  counter: function(value) {
    var vm = this;
    setTimeout(function() {
      vm.counter = 0;
    }, 2000);
  }
}
```
