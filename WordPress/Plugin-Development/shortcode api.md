## Shortcode API
A shortcode is a simple tag syntax between square brackets, such as `[something]` ,
used in posts. At render time when the post is displayed, the shortcode is dynamically replaced
with a more complex and user - defined content.

You must not register for your own use the following shortcodes: 
```
[wp_caption] [caption] [gallery] [embed]
```
These are registered by WordPress.

A simple plugin that uses `[book]` shortcode:
```php
/*
Plugin Name: Shortcode Example 1
Plugin URI: http://example.com/
Description: Replace [book] with a long Amazon link
Version: 1.0
Author: Ozh
Author URI: http://wrox.com/
*/
// Register a new shortcode: [book]
add_shortcode( 'book', 'boj_sc1_book' );
// The callback function that will replace [book]
function boj_sc1_book() {
  return '<a href="http://www.amazon.com/dp/0470560541">book</a>';
}
```
Add an attribute to the shortcode. In this example replace `[books title="xxx"]` with different Amazon links:
```php
...
// Register a new shortcode: [books title="xxx"]
add_shortcode( 'books', 'boj_sc2_multiple_books' );
// The callback function that will replace [books]
function boj_sc2_multiple_books($attr) {
  switch( $attr['title'] ) {
    case 'norm':
      $asin = '909090';
      $title = 'Volume 1';
      break;
    default:
    case 'pro':
      $asin = '0470560541';
      $title = 'Volume 2';
      break;
  }
  return "<a href='http://www.amazon.com/dp/$asin'>$title</a>";
}
```
