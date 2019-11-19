## Interactive SVG
SVGs have a Document Object Model so can be manipulated using Javascript in the same way you add interactivity to HTML.

It's also possible to add SVGs using the *<img>* tag and as a background-image in CSS, but neither of these methods allow 
you to manipulate the SVG with JS (or CSS).

Most commonly, you'll inline SVGs with external JS. This lets you to have separation of concerns, and easily reuse the 
JS for multiple SVGs on a website. However, you might already have the SVGs files, in which case it can be useful to 
embed them. You can have the JS embedded into external SVG files, so all the code is wrapped up together and can be 
emailed as a single file so the recipient can just open the SVG in their browser and have it work.

### Inline SVG Example
```html
<section class="section-block block-html">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 20" id="inline-1">
    <rect width="60" height="20" fill="#eee"></rect>
    <text font-size="5px" x="2" y="8">Inline SVG</text>
    <script type="text/javascript" async="" 
      src="http://www.google-analytics.com/ga.js">
    </script>
    <script type="text/javascript" async="" 
      src="https://www.gstatic.com/recaptcha/releases/75nbHAdFrusJCwoMVGTXoHoM/recaptcha__en.js">
    </script>
    <script type="text/javascript">
      var svg = document.getElementById('inline-1');
      console.log(svg);
    </script>
  </svg>
</section>
```

### External SVG Object Example (with internal JS)
```html
<section class="section-block block-html">
  <object data="https://example.com/external.svg" 
          type="image/svg+xml">
  </object>
</section>
```
external.svg
```
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 20" id="external">
  <rect width="80" height="60" fill="#eee"/>
  <text font-size="5px" x="2" y="8">External SVG Object</text>
  <script type="text/javascript"><![CDATA[
    var svg = document.getElementsByTagName('svg')[0];
    console.log(svg);
    var el = document.getElementById('item');
    var y = parseFloat(el.getAttributeNS(null, 'y'));
    el.setAttributeNS(null, 'y', y + 10);
  ]]></script>
</svg>
```
### Getting and Setting Attributes
Once you have selected an element, you can get and set its attributes with **getAttributeNS()** and **setAttributeNS()**.
```js
var y = parseFloat(element.getAttributeNS(null, 'y'));
element.setAttributeNS(null, 'y', y + 10);
```
This will work regardless how the SVG is added to the page or where the JS is. **NS** stands for namespace. Pass an 
additional parameter to each method, which can just be null.
#### External SVG example:
```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 20">
  <rect width="80" height="60" fill="#eee"/>
  <text id="item" font-size="5px" x="2" y="18">External SVG Object</text>
  <script type="text/javascript"><![CDATA[
    var svg = document.getElementsByTagName('svg')[0];
    var el = document.getElementById('item');
    var y = parseFloat(el.getAttributeNS(null, 'y'));
    el.setAttributeNS(null, 'y', y + 10);
  ]]></script>
</svg>
```
### Creating and Removing Elements
To create elements, you need to use the relevant document's *createElementNS()* method, passing in the SVG namespace 
and the tag name. You then will most likely want to add it to the SVG element with *appendChild()*. You can also use 
the *insertBefore()* or *insertAfter()* methods of an SVG element.
```js
var element = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
svg.appendChild(element);
```
Creating a text element that contains text is the same as it is in HTML: you have to create a separate text node 
using *createTextNode()*:
```js
var element = document.createElementNS('http://www.w3.org/2000/svg', 'text');
element.setAttributeNS(null, 'x', 5);
element.setAttributeNS(null, 'y', 15);
var txt = document.createTextNode("Hello World");
element.appendChild(txt);
svg.appendChild(element);
```
Removing an element is the same as it is in HTML. Get the element by id (or however), and then pass it into:
```js
var element = document.getElementById('item');
svg.removeChild(element);
```
