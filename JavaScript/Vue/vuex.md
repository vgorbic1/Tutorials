## Vuex
Vuex provides separation of concerns among components in the app. There is one file that stores application state.

![vuex1](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Vue/images/vuex1.jpg)

Put all Vuex related files in the `store` folder within `src` directory. Create a `store.js` file and put it to
the `store` folder. Install Vuex:
```
npm install --save vuex
```
Register the store in yuor `main.js` file:
```
import Vue from 'vue'
import App from './App.vue'

inport { store } from './store/store';

new Vue({
  el: '#app',
  store,
  render: h => h(App)
})
```
Update the `store.js` file:
```
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

new Vuex.Store({
    state: {
        
    }
})
```
### Getters
Getters allow for getting the current state of the app:
```
// store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex);

new Vuex.Store({
    state: {
        counter: 0
    },
    getters: {
        doubleCounter: state => {
            return state.counter * 2;
        }
    }
})
```
```
// Result.vue
<template>
    <p>Counter is: {{ counter }}</p>
</template>

<script>
    export default {
        computed: {
            counter() {
                return this.$store.getters.doubleCounter;
            }
        }
    }
</script>
```
### Actions
![actions](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Vue/images/vuex2.jpg)

Actions allows to add asynchronous tasks to mutations.
