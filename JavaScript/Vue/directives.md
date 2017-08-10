## Vue Internal Directives
### v-bind
`v-bind` tells the template to bind data to the HTML property. This directive accepts an argument that specifies
which attribute we need to bind:
```html
<a v-bind:href="link">Google</a>
```
```javascript
new Vue({
  ...
  data: {
    link: 'http://google.com'
  }
  ...
```
