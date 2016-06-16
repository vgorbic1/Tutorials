## Elements, Classes, and Selectors
In CSS, a pseudo-element is used to style parts of an element, for example:
- Styling the content ```::before``` or ```::after``` the content of an element.
- Using a pseudo class such as ```:hover``` to set the properties of an element when the user's mouse is touching the area of the element.

In Sass, the ```&``` character is used to specify exactly where a parent selector should be inserted. It also helps write psuedo classes in a much less repetitive way:
```
.notecard{ 
  &:hover{
      @include transform (rotatey(-180deg));  
    }
  }
```
will compile to the following CSS:
```
.notecard:hover {
  transform: rotatey(-180deg);
}
```

#### Mixin
In Sass, a mixin lets you make groups of CSS declarations that you want to reuse throughout your site.
```
@mixin backface-visibility {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -ms-backface-visibility: hidden;
  -o-backface-visibility: hidden;
}

...

 .notecard {
  .front, .back {
    width: 100%;
    height: 100%;
    position: absolute;

    @include backface_visibility;
  }
}
```
is equivalent to the following CSS:
```
.notecard .front, .notecard .back {
  width: 100%;
  height: 100%;
  position: absolute;

  backface-visibility: hidden;
  -webkit-backface-visibility: hidden; 
  -moz-backface-visibility: hidden;
  -ms-backface-visibility: hidden;
  -o-backface-visibility: hidden;
}
```
Mixin names and all other Sass identifiers use hyphens and underscores interchangeably.

Mixins also have the ability to take in a value. An argument, or parameter, is a value passed to the mixin that will be used inside the mixin, such as ```$visibility``` in this example:
```
@mixin backface-visibility($visibility) {
  backface-visibility: $visibility;
  -webkit-backface-visibility: $visibility;
  -moz-backface-visibility: $visibility;
  -ms-backface-visibility: $visibility;
  -o-backface-visibility: $visibility;
}
```
In fact, you should only ever use a mixin if it takes an argument. The syntax to pass in a value is as follows:
```
@include backface-visibility(hidden);
```

Mixin arguments can be assigned a default value in the mixin definition by using a special notation. A default value is assigned to the argument if no value is passed in when the mixin is included. Defining a default value for each argument is optional.
```
@mixin backface-visibility($visibility: hidden) {
   backface-visibility: $visibility;
  -webkit-backface-visibility: $visibility;
  -moz-backface-visibility: $visibility;
  -ms-backface-visibility: $visibility;
  -o-backface-visibility: $visibility;
}

...

@include backface-visibility;
```
In the example above, if no value is passed in when backface-visibility is included, hidden would be assigned to all properties.

In general, here are 5 important facts about arguments and mixins:
- Mixins can take multiple arguments.
- Sass allows you to explicitly define each argument in your @include statement.
- When values are explicitly specified you can send them out of order.
- If a mixin definition has a combination of arguments with and without a default value, you should define the ones with no default value first.
- Mixins can be nested.
Here are some concrete examples of the rules:
```
@mixin dashed-border($width, $color: #FFF) {
  border: {
     color: $color;
     width: $width;
     style: dashed;
  }
}

span { //only passes non-default argument
    @include dashed-border(3px);
}

p { //passes both arguments
    @include dashed-border(3px, green);
}

div { //passes out of order but explicitly defined
   @include dashed-border(color: purple, width: 5px); 
}
```
In the example above, the color of the border of span elements would be white, the border of paragraph elements would be green, while the div elements would have a thicker purple border.

Sass allows you to pass in multiple arguments in a list or a map format. For example, take the multiple properties needed to create the college-ruled stripes in the back of our notecard.
```
@mixin stripes($direction, $width-percent, $stripe-color, $stripe-background: #FFF) {
  background: repeating-linear-gradient(
    $direction,
    $stripe-background,
    $stripe-background ($width-percent - 1),
    $stripe-color 1%,
    $stripe-background $width-percent
  );
}
```
In this scenario, it makes sense to create a map with these properties in case we ever want to update or reference them.
```
$college-ruled-style: ( 
    direction: to bottom,
    width-percent: 15%,
    stripe-color: blue,
    stripe-background: white
);
```
When we include our mixin, we can then pass in these arguments in a map with the following ... notation:
```
.definition {
      width: 100%;
      height: 100%;
      @include stripes($college-ruled-style...);
 }
```
Remember to always prioritize readability over writing less code. This approach is only useful if you find it adds clarity to your codebase.

#### String Interpolation
In Sass, string interpolation is the process of placing a variable string in the middle of two other strings. In a mixin context, interpolation is handy when you want to make use of variables in selectors or file names. The notation is as follows:
```
@mixin photo-content($file) {
  content: url(#{$file}.jpg); //string interpolation
  object-fit: cover;
}

//....

.photo { 
  @include photo-content('titanosaur');
  width: 60%;
  margin: 0px auto; 
  }
```
String interpolation would enable the following CSS:
```
.photo { 
  content: url(titanosaur.jpg);
  width: 60%;
  margin: 0px auto; 
}
```
#### & selector
Sass allows ```&``` selector usage inside of mixins. The "&" selector gets assigned the value of the parent at the point where the mixin is included. If there is no parent selector, then the value is null and Sass will throw an error.
```
@mixin text-hover($color){
  &:hover {
      color: $color; 
  }
}
```
In the above, the value of the parent selector will be assigned based on the parent at the point where it is invoked.
```
 .word { // SCSS: 
    display: block; 
    text-align: center;
    position: relative;
    top: 40%;
    @include text-hover(red);
  }
```
The above will compile to the following CSS:
```
  .word{ 
    display: block;
    text-align: center;
    position: relative;
    top: 40%;
  }
  .word:hover{
    color: red;
  }
```
Notice that the mixin inherited the parent selector .word because that was the parent at the point where the mixin was included.
