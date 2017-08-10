## Styling
Several ways to get your template styled.

### :class
`:class` attaches a class to the HTML tag. Use an object `{}` syntax to 
use name of a css class as the key and true/false (displaying or not) as a value:
```html
<div :class="{red: true}"></div>
```
```css
.red {
  background-color: red;
}
```
You may attach the property to the class:
```html
<div :class="color"></div>
// you can also use array of classes:
// <div :class="[color, width, somethingelse]"></div>
```
```javascript
...
data {
  color: 'green'
}
...
```
```css
.green {
  background-color: green;
}
```

### :style
This directive changes the css style of the tag it is attached to:
```html
<div :style="{backgroundColor: color}"></div>
```
```javascript
...
data {
  color: 'gray'
}
...
```
```css
.gray {
  background-color: gray;
}
```
