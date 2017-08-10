## Simple String Interpolation
Use `{{ }}` for the string interpolation. It only works in place of text, not inside HTML selectors and properties!
```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <p>{{ title }}</p>
  <p>{{ sayHello() }}</p>
  <p>{{ sayHelloAgain() }}</p>
</div>
```
```javascript
new Vue({
  el: '#app',
  data: {
    title: 'Hello World!'
  },
  methods: {
    sayHello: function() {
      return 'Hello World!'
    },
    sayHelloAgain: function() {
      return this.title
    }
  }
});
```
Result
```
Hello World!

Hello World!

Hello World!
```
