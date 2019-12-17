## Install and Set Router
Install `react-router-dom` package.
```
npm install react-router-dom
  or
yarn add react-router-dom
```
Import `BrowserRouter` in index.js:
```javascript
// index.js
...
import { BrowserRouter } from 'react-router-dom';
```
Put the `BrowserRouter` component as a wrapper for the `App` component:
```javascript
// index.js
...
  <BrowserRouter>
    <App />
  </BrowserRouter>
...
```
### Create Routes
Import `Route` component from `react-router-dom` in `App.js`
```javascript
// App.js
...
import { Route } from 'react-router-dom';
...
```
Wrap page components into the `Route` component:
```javascript
// App.js
...
function App() {
  return (
    <div>
      <Route >
    </div>
...
```
### Create Sample Page Components
In the same `app.js` create page functional components:
```javascript
// App.js
...
const PageOne => () {
  <div><h1>Page One</h1></div>
}

const PageTwo => () {
  <div><h1>Page Two</h1></div>
}
...
```
Modify the `render()` code to apply routing:
```javascript
// App.js
...
function App() {
  return (
    <div>
      <Route exact path='/' component={PageOne} />
      <Route path='page-two' component={PageTwo} />
    </div>
...
```
Add a `Switch` component to display only one route from the list:
```javascript
// App.js
...
import { Switch, Route } from 'react-router-dom';
...
function App() {
  return (
    <div>
      <Switch>
        <Route exact path='/' component={PageOne} />
        <Route path='page-two' component={PageTwo} />
      </Switch>
    </div>
...
```
