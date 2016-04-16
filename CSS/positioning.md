## Positioning
The position property specifies the type of positioning method used for an element:
* **static** (Default. Normal flow)
* **relative** (Relative to its normal (ststic) position. Use top, bottom, left, right to position)
* **fixed** (Relative the browser window. Use top, bottom, left, right to position)
* **absolute** (Relative the ancestor element. Use top, bottom, left, right to position)
Elements are then positioned using the `top`, `bottom`, `left`, and `right` properties. However, these properties will not work unless the `position` property is set first. Thus, a "positioned" element is one whose position is anything except static.

#### position: static
`static` is a default positioning. Static positioned elements are not affected by the `top`, `bottom`, `left`, and `right` properties. Elements always positioned according to the normal flow of the page:
```
div.static {
    position: static;
}
```

#### position: relative
`relative` is positioned relative to its normal position. Setting the `top`, `right`, `bottom`, and `left` properties of a relatively-positioned element will cause it to be adjusted away from its normal position. Other content will not be adjusted to fit into any gap left by the element:
```
div.relative {
    position: relative;
    left: 30px;
}
```

#### position: fixed
`fixed` is positioned relative to the viewport, which means it always stays in the same place even if the page is scrolled. The `top`, `right`, `bottom`, and `left` properties are used to position the element. A fixed element does not leave a gap in the page where it would normally have been located.
```
div.fixed {
    position: fixed;
    bottom: 0;
    right: 0;
    width: 300px;
}
```

#### position: absolute
`absolute` is positioned relative to the nearest positioned ancestor. If an absolute positioned element has no positioned ancestors, it uses the document body, and moves along with page scrolling:
```
div.relative {
    position: relative;
    width: 400px;
    height: 200px;
    border: 3px solid #73AD21;
} 

div.absolute {
    position: absolute;
    top: 80px;
    right: 0;
    width: 200px;
}
```

#### z-index
When elements are positioned, they can overlap other elements. Use the `z-index` property to specify which element should be placed in front of, or behind, the others. An element can have a positive or negative stack order. Say, if `z-index` is -1, it will be placed behind the text. An element with greater stack order is always in front of an element with a lower stack order. If two positioned elements overlap without a `z-index` specified, the element positioned last in the HTML code will be shown on top.
```
img {
    position: absolute;
    left: 0px;
    top: 0px;
    z-index: -1;
}
```
