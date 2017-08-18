## Forms

### Basic Input
```html
<template>
...
<input type="text" v-model="email">
...
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
### Grouped Input
```html
<template>
...
<input type="text" v-model="userData.email">
...
<p>{{ uderData.email }}</p>
...
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
...
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
### Textarea
```html
<template>
...
<textarea v-model="message"></textarea>
...
<p>{{ message }}</p>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    message: 'Prepopulate the textarea'
  }
}
...
</script>
```
## Checkbox
```html
<template>
...
<div class="form-group">
 <label for="sendmail">
  <input
   type="checkbox"
   id="sendmail"
   value="SendMail"
   v-model="sendMail"> Send Mail
 </label>
 <label for="sendInfomail">
  <input
   type="checkbox"
   id="sendInfomail"
   value="SendInfoMail"
   v-model="sendMail"> Send Infomail
 </label>
</div>
...
<ul>
 <li v-for="element in sendMail">{{ element }}</li>
</ul>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    sendMail: []
  }
}
...
</script>
```
## Radio
```html
<template>
...
<div class="form-group">
 <label for="male">
  <input
   type="radio"
   id="male"
   value="Male"
   v-model="gender"> Male
 </label>
 <label for="female">
  <input
   type="radio"
   id="female"
   value="Female"
   v-model="gender"> Female
  </label>
</div>
...
<p>Gender: {{ gender }}</p>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    gender: 'Male'
  }
}
...
</script>
```
