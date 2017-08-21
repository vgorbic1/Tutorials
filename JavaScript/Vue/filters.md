## Filters
Filter transforms output in the template. It only transforms the output, not the data itself.

### Local Filter
Local filter works with the currenct template only.
```html
<template>
...
<p>{{ text | toUppercase }}</p>
...
</template>
```
```javascript
<script>
  ...
  data() {
    return {
      text: 'Hello there!'
    }
  },
  filters: {
    toUppercase(value) {
      return value.toUpperCase();
    }
  }
...
```
### Global Filter
Global filter works for entire application. Declare a new Vue instance in `main.js` file and use it as a filter.
```
...
<p>{{ text | toLowercase }}</p>
...
...
```
```javascript
...
Vue.filter(toLowercase, function(value) {
  return value.toLowerCase();
});
...
```
### Chain Filters
You can chain filters with the `|` pipe sign:
```html
<p>{{ text | toUppercase | toLowercase }}</p>
```
### Computed Property
Computed property is a better alternative to filters. Vue.js when recalculate the computed properties and this
helps better performance.
```html
<template>
...
<input v-model="filterText">
<ul><li v-for="fruit in filteredFruits">{{ fruit }}</li></ul>
...
</template>
```
```javascript
<script>
  ...
  data() {
    return {
      fruits: ['Apple', 'Banana', 'Mango'],
      filterText: ''
    }
  },
  computed: {
    filteredFruits() {
      return this.fruits.filter((element) => {
        return element.match(this.filterText);
      });
    }
  }
...
```

