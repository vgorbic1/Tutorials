## Components
Components extend Vue instances.

This is a simple component:
```html
...
<div id="app">
  <my-component></my-component>
</div>
...
```
```javascript
Vue.component('my-component', {
  data: funciton() {
    return {
      status: 'Critical'
    }
  },
  template: '<p>Server Status: {{ status }}</p>'
});

new Vue({
  el: '#app'
})
```
