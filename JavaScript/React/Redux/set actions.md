## Set an Action
Create a file `user.actions.js` in the `user` directory. This file will represent all actions for the store.
```javascript
// user.action.js
export const setCurrentUser = user => ({
  type: 'SET_CURRENT_USER', // reducer expects this string
  payload: user // set the object as a payload
});
```
  
