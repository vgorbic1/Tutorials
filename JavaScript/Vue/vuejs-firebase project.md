## Vuejs Firebase Strarter Project

### Firebase backend
- Create a new Firebase poject with [Firebase Console](https://console.firebase.google.com). You need a Google account for it.
Now, you can use the Firebase-powered backend for your application. It includes real-time database, authentication
mechanism, hosting, and analytics.
- Add database entry. (for example 'messages')
- For a simplicity change Rules to read and write publicly open:
```json
{
  "rules" : {
    ".read" : true,
    ".write" : true
  }
}
```

### Vue.js App
- Get Node.js installed to your local machine.
- Get Vue.js installed globally:
```
$ npm install -g vue-cli
```
- Go to the directory where you want to put your project and initialize a project with webpack.
You may use other templates. [more info](https://github.com/vuejs/vue-cli)
```
vue inint webpack yourprojectname
```
- Move to the project directory and install necessary packages:
```
cd yourprojectname
npm install
```
- Run your project on the developmnent server:
```
npm run dev
```
You should see the app running in your browser on port 8080

### Connect Vue.js with Firebase
- Install Firebase and VueFire packages locally into the project directory:
```
npm install firebase vuefire --save
```
- Have the Firebase project configuration info ready:
```
Firebase console -> Overview tab -> Project Settings -> "Add Firebase to your web app" button
```
- Go to main.js file of your local Vue.js project and add the following to the import section:
```
// main.js
import VueFire from 'vuefire'
Vue.use(VueFire)
```
- Import firebase to the app with the information from Firebase console:
```
// App.vue
<script>
  import Firebase from 'firebase'

  let config = {
    apiKey: 'YOUR_API_KEY',
    authDomain: 'YOUR_AUTH_DOMAIN',
    databaseURL: 'YOUR_DATABASE_URL',
    projectId: 'YOUR_PROJECT_ID',
    storageBucket: 'YOUR_STORAGE_BUCKET',
    messagingSenderId: 'YOUR_MESSAGING_SENDER_ID'
  }

  let app = Firebase.initializeApp(config)
</script>
```
- Obtain the reference to the database object:
```
// App.vue
<script>
  <...>
  let db = app.database()
  let messagesRef = db.ref('messages')
</script>
```
- Export the 'messages' object tin the Vue data objects to use inside tje template:
```
export default {
  firebase: {
    messages: messagesRef
  },
}
```
- Use Vue.js `v-for` directive to display all fields of the 'messages' object in the template:
```
// App.vue
<div v-for="message in messages">
  <h4>{{ message.title }}</h4>
  <p>{{ message.text }}</p>
  <p>{{ message.timestamp }}</p>
</div>
```
- Complete `App.vue` file:
```
// App.vue
<template>
  <div id="app">
    <div v-for="message in messages">
      <h4>{{ message.title }}</h4>
      <p>{{ message.text }}</p>
      <p>{{ message.timestamp }}</p>
    </div>
  </div>
</template>

<script>
  import Firebase from 'firebase'

  let config = {
    apiKey: 'YOUR_API_KEY',
    authDomain: 'YOUR_AUTH_DOMAIN',
    databaseURL: 'YOUR_DATABASE_URL',
    projectId: 'YOUR_PROJECT_ID',
    storageBucket: 'YOUR_STORAGE_BUCKET',
    messagingSenderId: 'YOUR_MESSAGING_SENDER_ID'
  }

  let app = Firebase.initializeApp(config)
  let db = app.database()
  let messagesRef = db.ref('messages')
  export default {
    name: 'app',
    firebase: {
      messages: messagesRef
    }
  }
</script>
```
