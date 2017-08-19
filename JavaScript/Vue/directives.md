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
Use the following shortcut for this directive:
```html
<a :href="link">Google</a>
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
Another example with `mousemove` event:
```html
<p v-on:mousemove="getCoordinates">{{ x }} / {{ y }}</p>
```
```javascript
new Vue({
  ...
  data: { x: 0, y: 0 }
  methods: function(event) { // the 'event' object is created by DOM
    this.x = event.clientX;
    this.y = event.clientY;
  }
  ...
```
You also can pass an argument(s) to the listener:
```html
<button v-on:click="increase(2)">Increase by 2</button>
// in order to pass the event and a custom argument use $event 
// v-on:click="increase(2, $event)"> ...
```
```javascript
...
  data { counter: 0 },
  methods: {
    increase: function(step) {
      this.counter += step;
    }
...
```
To modify event that is listened, use event modifier. For example for stopping propagation to the parent nodes
with a `.stop` modifier:
```html
... v-on:click.stop="" ...
```
Another option is to add a key modifier. For example you can fire up the `alertMe` method only when `enter` or 
`space` keys are pressed (released):
```html
<input type="text v-on:keyup.enter.space="alertMe">
```
Use a shortcut for this directive:
```html
<button @click="changeLink">Link</button>
```

### v-model
`v-model` directive allows for two-way binding:
```html
<input type="text" v-model="name">
<p>{{ name }}</p>
```
```javascript
new Vue ({
  ...
  data: {
    name: ''
  }
  ...
```

### v-text
`v-text` directive is used to display a string:
```html
<p v-text="'a string of text'"></p>
```
