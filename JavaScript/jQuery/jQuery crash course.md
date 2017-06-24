## jQuery Crash Course

### The jQuery Object
In old school JavaScript, to select elements that your CSS would simply call `#container a`, you may have written code like:
```js
document.getElementById('container').getElementsByTagName('a')
```
With jQuery, you can now simply write the following:
```js
$('#container a')
```
The dollar $ sign is a shortcut to the jQuery object.

### Syntax and Chaining
JQuery methods can be chained together, which will return the jQuery object:
```js
$('p.target')
 .css( { background:'#eef', border: '1px solid red' } )
 .click(function(){
  $(this)
  .css('background','#aaf')
  .animate(
   { width:'300px', borderWidth:'30px', marginLeft:'100px'},
   2000,
   function(){
    $(this).fadeOut();
   }
  );
 });
```
### No-Conflict Mode
jQuery is not the only JavaScript library to use the $ sign. For example, PrototypeJS uses $ as a
simple shortcut to the longer function `document.getElementById()`. To enable coexistence with other libraries,
write `jQuery( )` instead of each `$( )` or use a jQuery wrapper:
```js
jQuery('.something').each( function(){
  jQuery(this).addClass( 'stuff' );
});
jQuery.data( document.body, 'foo', 1337 );

 // or
 
// jQuery noConflict wrapper:
(function($) {
  // $() will work here
  $('.something').each( function(){
    $(this).addClass( 'stuff' );
  });
  $.data( document.body, 'foo', 1337 );
})(jQuery);
```
Both solutions are programmatically equal, but using a no - confl ict wrapper will enable you to more
conveniently and easily use existing code without having to replace each $ with a longer jQuery.

### Launching Code on Document Ready
A frequent requirement in JavaScript is to make sure that elements in a page load before you can do
something with them. As soon as the DOM hierarchy has been fully constructed, the document "ready" event
triggers: This happens before images load, before ads are shown, so the user experience is much
smoother and faster:
```js
jQuery(document).ready(function($) {
  // $() will work as an alias for jQuery() inside of this function
});
```
Using this technique, you can use the `$( )` syntax and be sure that you do not reference a DOM
element that has not been rendered by the browser yet.
