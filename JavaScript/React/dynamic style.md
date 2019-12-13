## Dynamic Styling
To bring to a child component a specific style element from the parent (via props):
```js
const MenuItem = ({ title, imageUrl, size }) => (
  <div className={menu-item}>
    <div style={{ backgroundImage: `url(${imageUrl})`}} />
  </div>
);
```
