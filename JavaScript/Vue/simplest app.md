## The Simplest App
Simple app that shows string interpolation with Vue instance:
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
The same app using a Vue component:
```html
<script src="https://unpkg.com/vue"></script>
<app-main></app-main>
```
```javascript
Vue.component('app-main', {
 data: function() {
   return {
     name: 'Vlad'
   }
 },
 template: '{{ name }}'
});
```
The same app using dinamic data binding:
```html
<script src="https://unpkg.com/vue"></script>
<app-main v-bind:name='Vlad'></app-main>
```
```javascript
Vue.component('app-main', {
 props: ['name'],
 template: '{{ name }}'
});
```
