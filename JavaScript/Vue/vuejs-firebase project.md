## Vuejs Firebase Strarter Project

### Firebase backend
- Create a new Firebase poject with [Firebase Console](https://console.firebase.google.com). You need a Google account for it.
Now, you can use the Firebase-powered backend for your application. It includes real-time database, authentication
mechanism, hosting, and analytics.
- Add database entry.
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
