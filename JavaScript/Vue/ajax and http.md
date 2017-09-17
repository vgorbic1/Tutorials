## Ajax and HTTP
Use *vue-resource* library for working with data on a server via HTTP.
```
npm install --save vue-resource
```
Configure the library in your application:
- import the package to the app in `main.js`.
- add a plugin to the core app functionality using `Vue.use` in `main.js`.
```
// main.js file
import Vue from 'vue'
import VueResource from 'vue-resource'
import App from './App.vue'

Vue.use(VueResource);

new Vue({
  el: '#app',
  render: h => h(App)
})
```

Use *Goggle Firebase* to test your backend.
- Don't forget to change the Rules (Database -> RULES):
```
{
  "rules": {
    ".read": "true",
    ".write": "true"
  }
}
```

### POST Data to Server
```
// App.vue
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label>Username</label>
                    <input type="text" 
                    v-model="user.username" class="form-control">
                </div>
                <div class="form-group">
                    <label>Email</label>
                    <input type="text"
                    v-model="user.email" class="form-control">
                </div>
                <button class="btn-btn-primary" @click="submit">Submit</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                user: {
                    username: '',
                    email: ''
                }
            };
        },
        methods: { 
            submit() {
                // Access HTTP object that comes with vue-resource lib
                this.$http.post('https://vuejs-http.firebaseio.com/data.json', this.user)
                    .then(response => {
                        console.log(response)
                    }, error => {
                        console.log(error);
                    });
            }
        }
    }
</script>
```
### GET Data from Server
```
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label>Username</label>
                    <input type="text" 
                    v-model="user.username" class="form-control">
                </div>
                <div class="form-group">
                    <label>Email</label>
                    <input type="text"
                    v-model="user.email" class="form-control">
                </div>
                <button class="btn-btn-primary" @click="submit">Submit</button>
                <hr>
                <button class="btn btn-primary" @click="fetchData">Get Data</button>
                <ul class="list-group">
                    <li class="list-group-item" v-for="u in users" :key="u">
                        {{ u.username }} - {{ u.email }}
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                user: {
                    username: '',
                    email: ''
                },
                users: []
            };
        },
        methods: { 
            submit() {
                // Access HTTP object that comes with vue-resource lib
                this.$http.post('https://vuejs-http-8f4b1.firebaseio.com/data.json', this.user)
                    .then(response => {
                        console.log(response)
                    }, error => {
                        console.log(error);
                    });
            },
            fetchData() {
                this.$http.get('https://vuejs-http-8f4b1.firebaseio.com/data.json')
                    .then(response => {
                        return response.json();
                    })
                    .then(data => {
                        const resultArray = [];
                        for (let key in data) {
                            resultArray.push(data[key]);
                        }
                        this.users = resultArray;
                    });
            }
        }
    }
</script>

<style>
</style>
```
### Set Global Options
In `main.js` set global options for the entire app. For example to set the url where all request will go:
```
// main.js
import Vue from 'vue'
import VueResource from 'vue-resource'
import App from './App.vue'

Vue.use(VueResource);
Vue.http.options.root = 'https://vuejs-http-8f4b1.firebaseio.com/data.json';

new Vue({
  el: '#app',
  render: h => h(App)
})
```
In the `App.vue` just use this root instead:
```
...
  submit() {
    // Access HTTP object that comes with vue-resource lib
    this.$http.post('', this.user).then(response => {
...
```
