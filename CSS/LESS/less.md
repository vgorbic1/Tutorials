## LESS

The browser would not be able to process and render the output, despite inheriting traits similar to CSS. The compiler will process the code and turn LESS syntax into browser-compliant CSS format. You can include less.js in your web site and it can compile all the linked .less stylesheets in real time, but this is slow and is not recommended. The recommended way is to compile your less stylesheets ahead of time and deploy a regular CSS file online.

#### Compilers
**Using JavaScript** (a slow and simplest way)
LESS comes with a less.js file. Create a stylesheet with .less extension and link it in your document:
```html
<link rel="stylesheet/less" type="text/css" href="main.less" />
```
Link CDN file with less.js script:
```
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.1/less.min.js"></script>
```
The LESS syntax will be compiled on the fly as the page loads. Keep in mind that using JavaScript is discouraged at the production stage, as it will badly affect the website performance.

**Using Comand-Line Interface**
LESS provides a native command line interface, lessc, which handles several tasks beyond just compiling the LESS syntax. Using the CLI we can lint the codes, compress the files, and create a source map. The command is based on Node.js that effectively allows the command to work across Windows, OS X, and Linux. Make sure that Node.js has been installed, then install LESS CLI through NPM (Node Package Manager) using the following command line:
```
npm install -g less
```
Now you have the lessc command at your disposal to compile LESS into CSS:
```
lessc style.less style.css
```

**Using Task Runner**
Use Grunt or Gulp tools to automatically compile less to css or use Graphical Interface Tools:
- Mixture 	OS X / Windows			Free
- Koala		OS X / Windows / Linux		Free
- Prepros		OS X / Windows			Freemium (USD29)
- WinLESS	Windows			Free
- CodeKit		OS X				USD32

#### Syntax
**Variables** The variables will allow us to store a constant value that later can be reused in the entire stylesheet.
```
@color-base: #2d5e8b;
.class1 {
    background-color: @color-base;
}
.class2 {
    background-color: #fff;
    color: @color-base;
}
.class3 {
    border: 1px solid @color-base;
}
```
When you want to change the color, we only need to change the value in this variable!

**Mixins** In LESS, we can use Mixins to reuse whole declarations in a CSS rule set in another rule set. Here is an example:
```
.gradients {
    background: #eaeaea; 
    background: linear-gradient(top, #eaeaea, #cccccc);
    background: -o-linear-gradient(top, #eaeaea, #cccccc); 
    background: -ms-linear-gradient(top, #eaeaea, #cccccc); 
    background: -moz-linear-gradient(top, #eaeaea, #cccccc); 
    background: -webkit-linear-gradient(top, #eaeaea, #cccccc); 
}
```
In the above snippet, we have preset a default gradient color inside the .gradients class. Whenever we want to add the gradients we simply insert the .gradients this way:
```
div {
    .gradients;
    border: 1px solid #555;
    border-radius: 3px;
}
```
Use Lesselements file as a library of preset CSS3 elements from here: [lesselements.com](http://lesselements.com) Include it in your less script:
```
@import "elements.less";
```
We can now reuse all the classes provided from the elements.less, for example, to add 3px border radius to a div, we can write:
```
div {
    .rounded(3px);
}
```

**Nested Rules** In LESS CSS, we can simplify the rule sets by nesting the child elements inside the parents. Say, you have this:
```
nav {
    height: 40px;
    width: 100%;
    background: #455868;
    border-bottom: 2px solid #283744;
}
nav li {
    width: 600px;
    height: 40px;
}
nav li a {
    color: #fff;
    line-height: 40px;
    text-shadow: 1px 1px 0px #283744;
}
```
In less it is more simple:
```
nav {
    height: 40px;
    width: 100%;
    background: #455868;
    border-bottom: 2px solid #283744;
    li {
        width: 600px;
        height: 40px;
        a {
            color: #fff;
            line-height: 40px;
            text-shadow: 1px 1px 0px #283744;
        }
    }
}
```
You can also assign pseudo-classes, like :hover, to the selector using the ampersand (&) symbol:
```
a {
    color: #fff;
    line-height: 40px;
    text-shadow: 1px 1px 0px #283744;
    &:hover {
        background-color: #000;
        color: #fff;
    }
}
```
**Operation.** It is possible to perform operations in LESS, such as addition, subtraction, multiplication and division to numbers, colors and variables in the stylesheet. Let’s say we want element B to be two times higher than element A. In that case, we can write it this way:
```
@height: 100px
.elementA {
    height: @height;    
}
.elementB {
    height: @height * 2;
}
```
**Scope** LESS applies the Scope concept, where variables will be inherited first from the local scope, and when it is not available locally, it will search through a wider scope.
```
header {
    @color: black;
    background-color: @color;
    nav {
        @color: blue;
            background-color: @color;
        a {
                color: @color;
        }
    }
}
```
In the example above, the header has a black background color, but nav‘s background color will be blue as it has the @color variable in its local scope, while the a will also have blue that is inherited from its nearer parent, nav.
