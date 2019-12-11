## How to Pass Props to a Child Component?
Props are parameters that are sent from the parent component to a child component.

### Pass Props

#### Parent
(Class component)
```js
...
render() {
  return (
    <div className='Parent'>
      <Child name={this.state.name} />
...
```

#### Child
(functional component)
```js
...
const Child = props => {
  return <h1>{props.name}</h1>
...
```
### Pass Children
Children are what you are passing in between of the brackets of the child (in
render() ) in the parent component. In the child component refer to them as `props.children`.
#### Parent
(Class component)
```js
...
render() {
  return (
    <div className='Parent'>
      <Child><h1>{this.state.name}</h1></Child>
...
```

#### Child
(functional component)
```js
...
const Child = props => {
  return <div>{props.children}</div>
...
```
