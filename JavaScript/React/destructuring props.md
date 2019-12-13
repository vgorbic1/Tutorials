## Destructuring Props
instead of
```js
const MenuItem = (props) => (
  <div className='menu-item'>
    <div className='content'>
      <h1 className='title'>{props.title}</h1>
      <span className='subtitle'>{props.subtitle}</span>
    </div>
  </div>
})
```
destructure the props:
```js
const MenuItem = ({title, subtitle}) => (
  <div className='menu-item'>
    <div className='content'>
      <h1 className='title'>{title}</h1>
      <span className='subtitle'>{subtitle}</span>
    </div>
  </div>
})
```
If a component needs one of many props, and others are passed to its child:
```js
const MenuItem = ({title, ...otherProps}) => (
  <div className='menu-item'>
    <div className='content'>
      <h1 className='title'>{title}</h1>
      <Button {...otherProps} />
    </div>
  </div>
})
```
