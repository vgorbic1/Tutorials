## Get Specific Route (URL)
To link a component with a specific url:
### Statically
Use `Link` component:
```javascript
...
import { Link } from 'react-router-dom';

...
  return (
    <div>
      <Link to='/home'>Home Page</Link>
...
```
### Dynamically
Use history props:
```javascript
...
  return (
    <div>
      <button onClick={ () => props.history.push('/home') }>Home Page</button>
...
```
This way you can use the component functions. The `history` prop is accessible only to
the direct child of the `Route` component:
```javascript
...
  <Route path='/page' component={Page} /> // only Page component has access to history prop
...
```
If you need to provide a dynamic link to multiple children deep, 
use a higher-order component `withRoute` to avoid props drilling:
```javascript
// child of child of child
...
import { withRouter } from 'react-router-dom';

const menuItem = ({ history }) => (
  <div onClick={ () => history.push('/page') } />
);
export default withRouter(MenuItem);
```
Or even better make it more dynamic with a `match` prop:
```javascript
...
import { withRouter } from 'react-router-dom';

const menuItem = ({ history, linkUrl, match }) => (
  <div onClick={ () => history.push(`${match.url}${linkUrl}`) } />
);
export default withRouter(MenuItem);
```

