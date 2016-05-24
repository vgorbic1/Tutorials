## LESS example:

elements.less file:
```
/*---------------------------------------------------
    LESS Elements 0.9
  ---------------------------------------------------
    A set of useful LESS mixins
    More info at: http://lesselements.com
  ---------------------------------------------------*/

.gradient(@color: #F5F5F5, @start: #EEE, @stop: #FFF) {
  background: @color;
  background: -webkit-gradient(linear,
                               left bottom,
                               left top,
                               color-stop(0, @start),
                               color-stop(1, @stop));
  background: -ms-linear-gradient(bottom,
                                  @start,
                                  @stop);
  background: -moz-linear-gradient(center bottom,
                                   @start 0%,
                                   @stop 100%);
  background: -o-linear-gradient(@stop,
                                 @start);
  filter: e(%("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=0)",@stop,@start));
}
.bw-gradient(@color: #F5F5F5, @start: 0, @stop: 255) {
  background: @color;
  background: -webkit-gradient(linear,
                               left bottom,
                               left top,
                               color-stop(0, rgb(@start,@start,@start)),
                               color-stop(1, rgb(@stop,@stop,@stop)));
  background: -ms-linear-gradient(bottom,
                                  rgb(@start,@start,@start) 0%,
                                  rgb(@stop,@stop,@stop) 100%);
  background: -moz-linear-gradient(center bottom,
                                   rgb(@start,@start,@start) 0%,
                                   rgb(@stop,@stop,@stop) 100%);
  background: -o-linear-gradient(rgb(@stop,@stop,@stop),
                                 rgb(@start,@start,@start));
  filter: e(%("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=0)",rgb(@stop,@stop,@stop),rgb(@start,@start,@start)));
}
.bordered(@top-color: #EEE, @right-color: #EEE, @bottom-color: #EEE, @left-color: #EEE) {
  border-top: solid 1px @top-color;
  border-left: solid 1px @left-color;
  border-right: solid 1px @right-color;
  border-bottom: solid 1px @bottom-color;
}
.drop-shadow(@x-axis: 0, @y-axis: 1px, @blur: 2px, @alpha: 0.1) {
  -webkit-box-shadow: @x-axis @y-axis @blur rgba(0, 0, 0, @alpha);
  -moz-box-shadow: @x-axis @y-axis @blur rgba(0, 0, 0, @alpha);
  box-shadow: @x-axis @y-axis @blur rgba(0, 0, 0, @alpha);
}
.rounded(@radius: 2px) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}
.border-radius(@topright: 0, @bottomright: 0, @bottomleft: 0, @topleft: 0) {
  -webkit-border-top-right-radius: @topright;
  -webkit-border-bottom-right-radius: @bottomright;
  -webkit-border-bottom-left-radius: @bottomleft;
  -webkit-border-top-left-radius: @topleft;
  -moz-border-radius-topright: @topright;
  -moz-border-radius-bottomright: @bottomright;
  -moz-border-radius-bottomleft: @bottomleft;
  -moz-border-radius-topleft: @topleft;
  border-top-right-radius: @topright;
  border-bottom-right-radius: @bottomright;
  border-bottom-left-radius: @bottomleft;
  border-top-left-radius: @topleft;
  .background-clip(padding-box);
}
.opacity(@opacity: 0.5) {
  -moz-opacity: @opacity;
  -khtml-opacity: @opacity;
  -webkit-opacity: @opacity;
  opacity: @opacity;
  @opperc: @opacity * 100;
  -ms-filter: ~"progid:DXImageTransform.Microsoft.Alpha(opacity=@{opperc})";
  filter: ~"alpha(opacity=@{opperc})";
}
.transition-duration(@duration: 0.2s) {
  -moz-transition-duration: @duration;
  -webkit-transition-duration: @duration;
  -o-transition-duration: @duration;
  transition-duration: @duration;
}
.transform(...) {
  -webkit-transform: @arguments;
  -moz-transform: @arguments;
  -o-transform: @arguments;
  -ms-transform: @arguments;
  transform: @arguments;
}
.rotation(@deg:5deg){
  .transform(rotate(@deg));
}
.scale(@ratio:1.5){
  .transform(scale(@ratio));
}
.transition(@duration:0.2s, @ease:ease-out) {
  -webkit-transition: all @duration @ease;
  -moz-transition: all @duration @ease;
  -o-transition: all @duration @ease;
  transition: all @duration @ease;
}
.inner-shadow(@horizontal:0, @vertical:1px, @blur:2px, @alpha: 0.4) {
  -webkit-box-shadow: inset @horizontal @vertical @blur rgba(0, 0, 0, @alpha);
  -moz-box-shadow: inset @horizontal @vertical @blur rgba(0, 0, 0, @alpha);
  box-shadow: inset @horizontal @vertical @blur rgba(0, 0, 0, @alpha);
}
.box-shadow(@arguments) {
  -webkit-box-shadow: @arguments;
  -moz-box-shadow: @arguments;
  box-shadow: @arguments;
}
.box-sizing(@sizing: border-box) {
  -ms-box-sizing: @sizing;
  -moz-box-sizing: @sizing;
  -webkit-box-sizing: @sizing;
  box-sizing: @sizing;
}
.user-select(@argument: none) {
  -webkit-user-select: @argument;
  -moz-user-select: @argument;
  -ms-user-select: @argument;
  user-select: @argument;
}
.columns(@colwidth: 250px, @colcount: 0, @colgap: 50px, @columnRuleColor: #EEE, @columnRuleStyle: solid, @columnRuleWidth: 1px) {
  -moz-column-width: @colwidth;
  -moz-column-count: @colcount;
  -moz-column-gap: @colgap;
  -moz-column-rule-color: @columnRuleColor;
  -moz-column-rule-style: @columnRuleStyle;
  -moz-column-rule-width: @columnRuleWidth;
  -webkit-column-width: @colwidth;
  -webkit-column-count: @colcount;
  -webkit-column-gap: @colgap;
  -webkit-column-rule-color: @columnRuleColor;
  -webkit-column-rule-style: @columnRuleStyle;
  -webkit-column-rule-width: @columnRuleWidth;
  column-width: @colwidth;
  column-count: @colcount;
  column-gap: @colgap;
  column-rule-color: @columnRuleColor;
  column-rule-style: @columnRuleStyle;
  column-rule-width: @columnRuleWidth;
}
.translate(@x:0, @y:0) {
  .transform(translate(@x, @y));
}
.background-clip(@argument: padding-box) {
  -moz-background-clip: @argument;
  -webkit-background-clip: @argument;
  background-clip: @argument;
}
```
style.less file:
```
// import less library from lesselements.com
@import "elements.less";

// Variable
@color-base: gray;

// Mixin
.gradients {
    background: #eaeaea; 
    background: linear-gradient(top, #eaeaea, #cccccc);
    background: -o-linear-gradient(top, #eaeaea, #cccccc); 
    background: -ms-linear-gradient(top, #eaeaea, #cccccc); 
    background: -moz-linear-gradient(top, #eaeaea, #cccccc); 
    background: -webkit-linear-gradient(top, #eaeaea, #cccccc); 
}

// Operation
@height: 50px;
	
h1 {
    .gradients;
    color: white;
	background-color: @color-base;
	height: @height * 2; // Use @height variable with mulriplication operation
}

h2 {
    color: @color-base;
	border: 1px solid @color-base;
	.rounded(10px); // this element's styling is taken from elements.less file
	height: @height;
}

h3 {
    color: red;
	border: 2px solid @color-base;
}
```
less.html
```html
<html>
<head>
<link rel="stylesheet/less" href="style.less"/>
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.1/less.min.js"></script>

</head>
<body>
<h1>This is a header</h1>
<h2>This is another header</h2>
<h3>This is still another header</h3>
</body>
</html>
```
