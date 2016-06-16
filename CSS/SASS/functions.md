## SASS Functions and Operations
Functions and operations in Sass allow for computing and iterating on styles. With Sass functions you can:
- Operate on color values
- Iterate on lists and maps
- Apply styles based on conditions
- Assign values that result from math operations

#### Colors
The alpha parameter in a color like RGBA or HSLA is a mask denoting opacity. It specifies how one color should be merged with another when the two are on top of each other. In Sass, the function fade-out makes a color more transparent by taking a number between 0 and 1 and decreasing opacity, or the alpha channel, by that amount:
```
   $color: rgba(39, 39, 39, 0.5);
   $amount: 0.1;
   $color2: fade-out($color, $amount);//rgba(39, 39, 39, 0.4)
```
The fade-in color function changes a color by increasing its opacity:
```
$color: rgba(55,7,56, 0.5);
$amount: 0.1;
$color2: fade-in($color, $amount); //rgba(55,7,56, 0.6)
```
The function ```adjust-hue($color, $degrees)``` changes the hue of a color by taking color and a number of degrees (usually between -360 degrees and 360 degrees), and rotate the color wheel by that amount.

#### Math
Sass also allows us to perform mathematical functions to compute measurements— including colors:
- The operation is performed on the red, green, and blue components. 
- It computes the answer by operating on every two digits.
```
$color: #010203 + #040506;
```
The above would compute piece-wise as follows:
```
01 + 04 = 05
02 + 05 = 07
03 + 06 = 09
```
and compile to:
```
color: #050709;
```
Sass arithmetic can also compute HSLA and string colors such as red and blue.

The Sass arithmetic operations are:
- addition +
- subtraction -
- multiplication *
- division /, and
- modulo %.
Modulo, or ```%```, is the remainder in a given division, so "9%2" would be "1".

SCSS arithmetic requires that the units are compatible; for example, you can't multiply pixels by ems. Also, just like in regular math, multiplying two units together results in squared units:10px * 10px = 100px * px. Since there is no such thing as squared units in CSS, the above would throw an error. You would need to multiply 10px * 10 in order to obtain 100px.

In CSS the / character can be used as a separator. In Sass, the character is also used in division. Here are the specific instances / counts as division:
- If the value, or any part of it, is stored in a variable or returned by a function.
- If the value is surrounded by parentheses, unless those parentheses are outside a list and the value is inside.
- If the value is used as part of another arithmetic expression.
```
width: $variable/6; //division
line-height: (600px)/9; //division
margin-left: 20-10 px/ 2; //division
font-size: 10px/8px; //not division
```

#### Loops
Beyond the simple math and color transformations we explored in the previous exercises, Sass also allows for more complex functions. *Each* loops in Sass iterate on each of the values on a list:
```
@each $item in $list {
  //some rules and or conditions
}
```
The value of $item is dynamically assigned to the value of the object in the list according to its position and the iteration of the loop.

*For* loops in Sass can be used to style numerous elements or assigning properties all at once. They work like any for-loop you've seen before.
```
@for $i from $begin through $end {
   //some rules and or conditions
}
```
In the example above:
- $i is just a variable for the index, or position of the element in the list.
- $begin and $end are placeholders for the start and end points of the loop.
- The keywords through and to are interchangeable in Sass.
For-loops are useful for many things, but in the following exercises we will be using them to style a block of rainbow divs!
```
$total: 10; //Number of .ray divs in our html
$step: 360deg / $total; //Used to compute the hue based on color-wheel

.ray {
  height: 30px;
}

@for $i from 1 through $total {
   .ray:nth-child(#{$i}){
      background: adjust-hue(blue, $i * $step);
   }
}
```

#### If
In Sass, ```if()``` is a function that can only branch one of two ways based on a condition. You can use it inline, to assign the value of a property:
```
width: if( $condition, $value-if-true, $value-if-false);
```
For cases with more than two outcomes, the ```@if```, ```@else-if```, and ```@else``` directives allow for more flexibility.
```
@mixin deck($suite) {
 @if($suite == hearts || $suite == spades){
   color: blue;
 }
 @else-if($suite == clovers || $suite == diamonds){
   color: red;
 }
 @else{
   //some rule
 }
}
```
The mixin above is a good example for how we would want to handle the coloring of a deck of cards based on a suite condition.
