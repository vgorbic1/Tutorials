## Forms

### Basic Input
```html
<template>
...
<input type="text" v-model="email">
<p>{{ email }}</p>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    email: ''
  }
}
...
</script>
```
### Groped Input
```html
<template>
...
<input type="text" v-model="userData.email">
<p>{{ uderData.email }}</p>
<input type="text" v-model="userData.username">
<p>{{ uderData.username }}</p>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    userData: {
      email: '',
      username: ''
    }
  }
}
...
</script>
```
### Modifiers
Use modifiers to set the time when the model response to the change. It is possible to chain the modifiers.
#### Lazy
This modifier will make the data updated only when the field goes out of the focuse:
```html
<template>
...
<input type="text" v-model.lazy="email">
<p>{{ email }}</p>
...
</template>
```
#### Number
This modifier will force to convert the input into the number as a value for the field data.
#### Trim
This modifier automatically trim user's input, stripping white spaces in the beginning and the end of the input.
```html
...
<input type="text" v-model.lazy.trim="email">
...
```
