## Filters
Filter transforms output in the template.

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
