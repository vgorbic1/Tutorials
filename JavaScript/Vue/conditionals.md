## Condationals
Use the following elements when you need to conditinally show certain elements on the page.

### v-if
Use this directive to show the elment conditionally. It attaches or detaches the element from the DOM.
```html
<p v-if="show">You can see me</p>
<button @click="show = !show">Switch</button>
```
```javascript
...
data {
  show: true
}
...
```

### v-else
Use this directive to show an element of the page when the `v-if` condition is `false`:
```html
<p v-if="show">You can see me</p>
<p v-else>Now you can see me</p>
<button @click="show = !show">Switch</button>
```
```javascript
...
data {
  show: true
}
...
```

### &lt;template&gt;
Use HTML tag `<template>` in order to group elements:
```html
<template v-if="show">
  <p>Show me</p>
</template>
```

### v-show
Use this directive, if you want just hide the element, not remove it from the DOM:
```html
<p v-show="show">Hide me</p>
```
