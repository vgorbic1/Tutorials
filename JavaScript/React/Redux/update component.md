## Upadate a Component after State Change
Anytime we need properties from our root reducer (state) we will have the `connect()` function.
In the component file import the `connect` function from Redux:
```js
import { connect } from 'react-redux';
...
```
Connect is a higher level component that lets us modify the base component to
give us access to Redux functionality.

Set the export with the connect:
```js
...
export default connect()(Header);
```
Put the function that allows us to access the state (root reducer) as the second parameter of the `conntect`:
```js
...
const mapStateToProps = state => ({ // where state is just the root reducer object
  currentUser: state.user.currentUser
});

export default connect(mapStateToProps)(Header);
```
