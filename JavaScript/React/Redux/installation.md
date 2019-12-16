## Installation

Redux is usually installed with three libraries:
```
yarn add redux redux-logger react-redux
  or
npm install redux redux-logger react-redux
```
Put *Provider* component to the index.js file:
```javascript
// index.js
import { Provider } from 'react-redux';
```
This component wrapps entire application. It should be the parent of everything inside the app.
```javascript
...
ReactDOM.render(
  <Provider>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </Provider>
...
```
Have a new directory `redux` to put the Store in. Inside that directory put root.reducer.js file that
holds the entire State. Create another directory within `redux` that represents a particular State segment 
reducer, say `user`. Inside that directory put user.reducer.js file that holds the `User` related state.
```
/redux
  root.reducer.js
  /user
    user.reducer.js
```
