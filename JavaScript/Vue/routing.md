## Routing
Install a router package:
```
npm install --save vue-router
```
Import the router in the `main.js` file:
```
import Vue from 'vue'
import VueRouter from 'vue-router'
import App from './App.vue'

Vue.use(VueRouter);

new Vue({
  el: '#app',
  render: h => h(App)
})
```
Create a new file in `src` directory and call it `routes.js`:
```
import Home from './components/Home.vue'
import User from './components/user/User.vue'

export const routes = [
    { path: '', component: Home },
    { path: '/user', component: User }
];
```
Register this new file in `main.js`:
```
import Vue from 'vue'
import VueRouter from 'vue-router'
import App from './App.vue'
import { routes } from './routes'

Vue.use(VueRouter);

const router = new VueRouter({
  routes
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```
In `App.vue` mark the place where components showld be loaded by the router using `<router-view>`:
```
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Routing</h1>
                <hr>
                <router-view></router-view>
            </div>
        </div>
    </div>
</template>
```
Make your server always return index.html. Even if the page is not found (404 Error), since the routing is handled
by VueJS application which is entered via index.html. After that make sure that you have swiched from the default *hash* mode
to the mode *history* in the `main.js` file:
```
...
const router = new VueRouter({
  routes,
  mode: 'history'
});
...
```
Use `router-link` to set up links in your component. Make sure you have an `active-class` attribute for each item:
```
<template>
  <ul class="nav nav-pills">
      <router-link to="/" tag="li" active-class="active" exact><a>Home</a></router-link>
      <router-link to="/user" tag="li" active-class="active"><a>User</a></router-link>
  </ul>
</template>
```
To navigate directly from your code:
```
<template>
    <div>
        <h1>The User Page</h1>
        <button @click="navigateToHome" class="btn btn-primary">Go Home</button>
    </div>
</template>

<script>
export default {
  methods: {
      navigateToHome() {
          this.$router.push('/');
      }
  }
}
</script>
```
Passing dynamic piecse with url use this syntax in `routes.js` in your 'path':
```
export const routes = [
    { path: '', component: Home },
    { path: '/user/:id', component: User }
];
```
To retrieve a dynamic component (`id` in this case):
```
<template>
    <div>
        <h1>The User Page</h1>
        {{ id }}
    </div>
</template>

<script>
export default {
    data() {
        return {
            id: this.$route.params.id
        }
    }
}
</script>
```
### Nested Routes
Create child routs (subrouts) in your `routes.js` file:
```
export const routes = [
    { path: '', component: Home },
    { path: '/user', component: User, children: [
        { path: '', component: UserStart },
        { path: ':id', component: UserDetail },
        { path: ':id/edit', component: UserEdit }
    ] }
];
```
Add the `<router-view`> to the component (`User.vue`):
```
<template>
    <div>
        <h1>The User Page</h1>
        <router-view></router-view>
    </div>
</template>
```
To load the nested routs (childern) link them using `<router-link>`:
```
<template>
    <div>
        <p>Please select a User</p>
        <hr>
        <ul class="list-group">
            <router-link 
                tag="li" 
                to="/user/1"
                class="list-group-item" >User 1</router-link>
            <router-link 
                tag="li" 
                to="/user/2"
                class="list-group-item" >User 2</router-link>
            <router-link 
                tag="li" 
                to="/user/3"
                class="list-group-item" >User 3</router-link>
        </ul>
    </div>
</template>
```
To "extract" data from the route:
```
<template>
    <div>
        <h3>Some User Details</h3>
        <p>User Loaded has ID: {{ $route.params.id }}</p>
    </div>
</template>
```
To add a dynamic link (in our case in `UserDetail.vue` subcomponent):
```
<template>
    <div>
        <h3>Some User Details</h3>
        <p>User Loaded has ID: {{ $route.params.id }}</p>
        <router-link 
            class="btn btn-primary"
            tag="button"
            :to="'/user/' + $route.params.id + '/edit'">
            Edit User</router-link>
    </div>
</template>
```
### Named Routers
Identify a route by adding a name to it in `routes.js`:
```
...
export const routes = [
    ...
    { path: '/user', component: User, children: [
        { path: ':id/edit', component: UserEdit, name: `userEdit`}
    ] }
];
```
use this name in the component:
```
<template>
    <div>
        <h3>Some User Details</h3>
        <p>User Loaded has ID: {{ $route.params.id }}</p>
        <router-link 
            class="btn btn-primary"
            tag="button"
            :to="{ name: 'userEdit', params: { id: $route.params.id } }">
            Edit User</router-link>
    </div>
</template>
```
