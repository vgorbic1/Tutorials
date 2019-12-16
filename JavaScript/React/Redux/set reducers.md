## Set a Reducer
Reducer is just a function that takes a current state and action adn returns updated state.
```javascript
// user.reducer.js

// set initial state:
const INITIAL_STATE = {
  currentUser: null
}

// set initial state as default parameter. If the state is NULL, 
// it is still considered to be a valid state,
// and the default parameter will not be used.
const userReducer = (state = INITIAL_STATE, action) => { 
  // set a switch to return either modified state or current one
  switch (action.type) {
    // in case of the existing action named SET_CURRENT_USER
    case 'SET_CURRENT_USER':
      return {
        ...state, // all existing state object propeties
        currentUser: action.payload // the property to update
      }
    // if there is no action named SET_CURRENT_USER
    default:
      return state; // just return the current state
  }
}

// export the reducer as a default value
export default userReducer;
```
Combine this reducer (with others) in the root reducer
```javascript
// root-reducer.js

// import function that comes with Redux
import { combineReducers } from 'redux';

// import a reducer that should be combined
import userReducer from './user/user.reducer';

// the key of the object represent the slice of state
export default combinedReducers({
  user: userReducer
});
```
