## CSS Basics:
```css
p {
  color: blue;
}
```
- **p** - selector
- **color: blue;** - declaration
- **color** - property
- **blue** - value
```css
a:hover {
  color: blue;
}
```
- **:hover** - pseudo class
```css
a:before {
  content: url(image.png);
```
- **:before** - pseudo element. The element, which does not exists when HTML is rendering. It is attached later.

### Display
There are two types of tags (elements)
- `inline elements` take the only space they need
- `block elements` take the entire line.
```css
display: block // makes the element to be a block element.
display: inline // makes the element to be inline element.
display: inline-block // visually it it an inline element but you may upply width and height properties to it.
display: flex // New in CSS3. Used for positioning elements within a container with flex properties.
didplay: none // removes the element from the view.
