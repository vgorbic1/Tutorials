## SASS
Sass, or Syntactically Awesome StyleSheets, is an extension language for CSS. With Sass, you can write clean, sustainable CSS code and solve the common repetition and maintenance challenges present in traditional CSS.

Sass can't be directly interpreted by your browser, so it must first be converted, or compiled, to CSS before the browser can directly understand it. Compiling refers to converting code to lower level code so that it can be executed. By compiling SCSS to CSS, it can be interpreted by your browser and the results will appear on a webpage.

Compile it to CSS by typing the following command in the terminal and pressing enter:
```
sass main.scss main.css
```
The sass command above takes in two arguments:
- The input (main.scss)
- The location of where to place that output (main.css)

#### Nesting
Nesting is the process of placing selectors inside the scope of another selector. In Sass, it's helpful to think of the scope of a selector as any of the code between its opening { and closing } curly brackets. Selectors that are nested inside the scope of another selector are referred to as children. The former selector is referred to as the parent. This is just like the relationship observed in HTML elements. Nesting allows you to see the clear DOM relationship between two selectors while also removing the repetition observed in CSS.
```
.parent {
  color: blue;
  .child {
    font-size: 12px;
  }
}
```
compiles to
```
.parent {
  color: blue;
}

.parent .child {
    font-size: 12px;
}
```
In SCSS, nesting is not limited only to selectors. You can also nest common CSS properties if you append a : colon suffix after the name of the property:
```
.parent {
  font : {
    family: Roboto, sans-serif;
    size: 12px;
    decoration: none;
  }
}
```
will compile to the following CSS:
```
.parent{
  font-family: Roboto, sans-serif;
  font-size: 12px;
  font-decoration: none;
}
```

#### Variables
Variables in SCSS allow you to assign an identifier of your choice to a specific value. Unlike in CSS, if you need to tweak a value, you'll only have to update it in one place and the change will be reflected in multiple rules. In Sass, ```$``` is used to define and reference a variable:
```
$translucent-white: rgba(255,255,255,0.3);
```
It's important to stick to one naming convention for variables when you first build out your codebase. This will help you reference them easily in the future.

There are different data types you can assign to a variable in CSS. n addition to the color data type we have seen, there are also:
- Numbers, such as 8.11, 12, and 10px. Notice that while 10 has a unit of px associated with it, it is still considered a number.
- Strings of text, with and without quotes. Some examples are "potato", 'tomato', span.
- Booleans, or simply true and false.
- null, which is considered an empty value.
```
$icon-square-length: 300px; // put this line on the top of your scss file

.icon {
    width: $icon-square-length;
    height: $icon-square-length;
}
```

#### Lists and Maps
In addition to color, numbers, strings, booleans, and null, Sass also has two other data types, lists and maps. Lists can be separated by either spaces or commas. For example, the following list denotes font properties, such as ```1.5em Helvetica bold;``` or ```Helvetica, Arial, sans-serif``` You can also surround a list with parentheses and create lists made up of lists.

Maps are very similar to lists, but instead each object is a key-value pair. The typical map looks like: ```(key1: value1, key2: value2)``` In a map, the value of a key can be a list or another map.
```
$standard-border: 4px solid black; // put this line on the top of your scss file
  // Find all of the instances that use `4px solid black` in main.scss and replace them with 
  // the $standard-border variable reference. 
.icon {
    border: $standard-border;
}
```
