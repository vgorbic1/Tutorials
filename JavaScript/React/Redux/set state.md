## Set State through a Component (dispatch an action)
To set a new State within a component, bring `connect()` higher level component:
```js
import { connect } from 'react-redux';
...
```
Also import the action that triggers the state change:
```js
...
import { setCurrentUser } from './redux/user/user.actions';
...
```
Use the export with the `connect` function and `mapDispatchToProps`:
```js
...
const mapDispatchToProps = dispatch => ({
  setCurrentUser: user => dispatch(setCurrentUser(user))
});

export default connect(null, mapDispatchToProps)(App);
```
