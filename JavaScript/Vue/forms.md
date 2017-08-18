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
### Select
```html
<template>
...
<select id="priority"
  class="form-control"
  v-model="selectedPriority">
  <option v-for="priority in priorities">
    {{ priority }}
  </option>
</select>
...
<p>Priority: {{ selectedPriority }}</p>
...
</template>
```
```javascript
<script>
...
data() {
  return {
    selectedPriority: 'High',
    priorities: ['High', 'Medium', 'Low']
  }
}
...
</script>
```
To get a `selected` property set use the following:
```html
<template>
...
  <option v-for="priority in priorities" :selected="priority == 'Medium'">
    {{ priority }}
  </option>
...
</template>
```
### Custom Input
This is what `v-model` directive does behind the scenes:
```
 v-model="email"
   is the same as
 v-bind:value="email"
 @input="email = $event.target.value"
 ```
 The best way to create a custom input is by creating a new component and putting
 the code there:
 ```
 // Switch.vue
 <template>
    <div>
        <div
                id="on"
                @click="switched(true)"
                :class="{active: value}">On</div>
        <div
                id="off"
                @click="switched(false)"
                :class="{active: !value}">Off</div>
    </div>
</template>

<script>
    export default {
        props: ['value'],
        methods: {
            switched(isOn) {
                this.$emit('input', isOn);
            }
        }
    }
</script>

<style scoped>
    #on, #off {
        width: 40px;
        height: 20px;
        background-color: lightgray;
        padding: 2px;
        display: inline-block;
        margin: 10px -2px;
        box-sizing: content-box;
        cursor: pointer;
        text-align: center;
    }

    #on:hover, #on.active {
        background-color: lightgreen;
    }

    #off:hover, #off.active {
        background-color: lightcoral;
    }
</style>
```
```
// App.vue
<template>
    <div class="container">
        <form>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <app-switch v-model="dataSwitch"></app-switch>
                </div>
            </div>
        </form>
        <hr>
        <div class="row" v-if="isSubmitted">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <div class="panel panel-default">
                    <div class="panel-heading">
                        <h4>Your Data</h4>
                    </div>
                    <div class="panel-body">
                        <p>Switched: {{ dataSwitch }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Switch from './Switch.vue';

    export default {
        data () {
            return {
                dataSwitch: true,
                isSubmitted: false
            }
        },
        methods: {
          submitted() {
              this.isSubmitted = true;
          }
        },
        components: {
            appSwitch: Switch
        }
    }
</script>

<style>
</style>
```
### Submit
Use `prevent` modifier to prevent the button from submitting the form to the server:
```
<button @click.prevent="submitted">Submit</button>
```
This is the entire code:
```
<template>
...
<button @click.prevent="submitted">Submit</button>
...
</template>
<script>
  data() {
    ...
    isSubmitted: false
  },
  methods: {
    submitted() {
      this.isSubmitted = true;
      // more code if the form is submitted
    }
  ...
```
