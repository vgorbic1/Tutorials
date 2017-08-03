## The Simplest App
Simple app that shows string interpolation with Vue framework.
```html
<script src="https://unpkg.com/vue"></script>
<div id="app">
  {{ name }}
</div>
```
```javascript
new Vue({
  el: '#app',
  data: {
    name: 'Vlad'
  }
});
```
