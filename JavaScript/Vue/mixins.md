## Mixins
Mixins allows to reuse code in different components.

### Local Mixin
Put a mixin with the needed code in a separate file:
```javascript
// fruitMixin.js
export const fruitMixin = {
  data() {
    fruits: ['Apple', 'Banana', 'Mango'], 
    fileterText: ''
  },
  computed: {
    filteredFruits() {
      return this.fruits.filter(element) => {
        return element.match(this.filterText);
      });
    }
  }
}
```
Now we can import this code to any component:
```javascript
<script>
import { fruitMixin } from './fruitMixin';
export default {
  mixins: [fruitMixin]
}
...
```

### Global Mixin
Global mixin got registered in all components! Use it with caution.
