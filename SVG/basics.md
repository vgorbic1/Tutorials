## SVG Basics

SVGs are Scalable Vector Graphics. The advantage of this approach is that it makes graphics Scalable: you can zoom in 
on the image as much as you like and it will never pixelate because the image will be re-rendered after each zoom.

SVG is based on XML so consists of a series of nested elements within an SVG element. You can create an svg file by 
creating a new text file and changing its file extension to .svg. You can edit its contents in any text-editor.

As stated at the beginning of this post, an SVG consists of element inside an SVG element. An SVG must therefore 
start with *<svg>* and end with *</svg>*. Often SVGs will start with a DOCTYPE declaration, but according to these 
[SVG authoring guidelines](https://jwatt.org/svg/authoring/) there's no need. Those guidelines suggest that you include *version="1.1"* and 
*baseProfile="full"* but it's not really necessary.

You can include *height* and *width* attributes to give the SVG a fixed size, otherwise it will fill the 
available space. You can use the *viewBox* attribute to define the range of values shown in the SVG.

### Example Line
 A line is defined by the attributes x1, y1, x2 and y2:
 ```xml
 <svg xmlns="http://www.w3.org/2000/svg">
    <line
        x1="40" y1="30"
        x2="240" y2="100"
        stroke="black" />
</svg>
```

[SVG authoring guidelines](https://jwatt.org/svg/authoring/)
