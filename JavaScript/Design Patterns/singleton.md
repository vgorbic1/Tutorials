## Singleton Pattern
Singleton returns only one instance of an object at a time.
```javascript
const Singleton = (function() {
  let instance;

  function createInstance() {
    const object = new Object({name:'John'});
    return object;
  }

  return {
    getInstance: function() {
      if(!instance){
        instance = createInstance();
      }
      return instance;
    }
  }
})();

const instanceA = Singleton.getInstance();
const instanceB = Singleton.getInstance(); // is the same instance!
console.log(instanceA === instanceB);
```
