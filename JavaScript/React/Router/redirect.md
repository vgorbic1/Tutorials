## Conditional Redirect
- To redirect to a specific component (page) according to the conditional statement use *Redirect* component:
```js
...
{ Route, Redirect } from 'react-router-dom';
...
```
- Get the value to evaluate from the Stare of Redux Store
- Inside the switch create the conditional statement:
```js
...
  <Route exact path='/signin' 
               render={ () => this.props.currentUser ? (<Redirect to='/'>) : (<SignIn />) } />
...
```
