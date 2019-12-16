## Set the Store
To set the store put the `store.js` file into the `redux` directory.
```javascript
// store.js
import {createStore, applyMiddleware } from 'redux';

// import a logger as middleware which is useful for debugging
import logger from 'redux-logger';

import rootReducer from './root-reducer';

// set middleware; include others as the array elements
const middlewares = [logger];

// create store
const store = createStore(rootReducer, applyMiddleware(...middlewares));
export default store;
```
pass this store object to the provider in `index.js`:
```javascript
...
import store from './redux/store';

ReactDOM.render(
  <Provider store={store}>
    <BrowserRouter>
...
```
