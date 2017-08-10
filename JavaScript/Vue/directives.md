## Vue Build-in Directives
Directive is an instruction you place in your code. Vue shipps with a few build-in directives. There is a way
to write custom directives, though.

### v-bind
`v-bind` tells the template to dynamically bind data to the HTML tag. This directive accepts an argument that specifies
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

### v-once
`v-once` allows the tag NOT to be updated (changed) if it is got changed later, say somewhere in methods:
```html
<h1 v-once>{{ title }}</h1>
```
```javascript
new Vue({
  ...
  data: {
    title: Hello!
  },
  methods: {
    changeTitle: function() {
      this.title = "Bye!";
      return this.title;
    }
  }
});
```
### v-html
`v-html` allows to pass HTML code into the HTML attribute without escaping HTML chalarcters:
```html
<p v-html="htmlLink"></p>
```
```javascript
new Vue({
  ...
  data {
    htmlLink: '<a href="http://google.com">Google</a>'
  }
  ...
```
### v-on
Use `v-on` as a listener to some events coming from the template. The argument is the name of the event we want to consume.
```html
<button v-on:click="increase">Click Here</button>
```
```javascript
new Vue({
  ...
  data {
    counter: 0
  },
  methods: {
    increase: function() {
      this.count++;
    }
  ...
```
