## Outputing Lists

### v-for
To output lists use `v-for` directive. It replicates the element on which it sits.
```html
<ul>
  <li v-for="ingredient in ingredients">{{ ingredient }}</li>
</ul>
```
```javascript
...
data: {
  ingredients: ['meat', 'fruit', 'cookies']
}
...
```

To extract the array index of the current item in the loop use `( )` with two arguments. The order
of the arguments is important! The first one is the name of the element, the second is its index:
```html
<li v-for="(ingredient, i) in ingredients">
```

Use `<template>` tag to group the repeated elements:
```html
<template v-for="(ingredient, i) in ingredients">
  <p>{{ ingredient }}</p>
  <p>({{ i }})</p>
</template>
```

To loop through numbers:
```html
<span v-for="n in 10">{{ n }}</span>
```

To be safe, assign a unique kety to each element in the array (loop):
```html
<ul>
  <li v-for="ingredient in ingredients" :key="ingredient">{{ ingredient }}</li>
</ul>
