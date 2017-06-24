## A Proper Way to Include Scripts
The main function you use to insert JavaScript into a WordPress page is `wp_enqueue_script()`,
which as it name suggests adds a script to a queue of required scripts.
The goal of `wp_enqueue_script()` is to register a script and tell WordPress to properly inject it in
the page. The function syntax and its five arguments follow:
```php
// Add a script to the insert queue
wp_enqueue_script( $handle, $src, $dependencies, $ver, $in_footer );
```
- `$handle` — The only mandatory argument of the function, this represents the name of
the script in the form of a lowercase string. The name of the script is either provided by
WordPress or is a custom name registered by your plugin. In such a case, you should of
course make it unique.
- `$src` — If provided, this is the URL of the script. WordPress needs this parameter only if
it does not know this script yet. If the script is already known, this parameter will be simply
ignored.
- `$dependencies` — An optional array of handles the script you want to add depends on and
as such that must be loaded before. This parameter is needed only if WordPress does not
know about this script.
- `$ver` — An optional version number, in the liberal form of a string such as 1.0 or 3.0.1 - RC1.
This makes sure the browser fetches the correct version of a script, regardless of its caching
settings.
- `$in_footer` — An optional Boolean you set to true if instead of having your script injected
into the <head> of the document, you want it placed at the bottom of the page near the
closing </body> tag.

1. No matter how many plugins require the same script, it will be added only once into the page.
2. You can precisely select on what page you want to add your script.
3. Specifying dependencies as described next, you can expressly set the order in which several
scripts will be included in the page, no matter the sequence of `wp_enqueue_script()`
function calls.
4. Scripts are added in compliance to the `FORCE_SSL_ADMIN` constant value. (That is, if the
user uses WordPress over https in the admin area, scripts will be added over https, too.)

Typically, you will use `wp_enqueue_script()` hooked to an early action that occurs before any
content is sent to the browser:
```php
add_action( 'init', 'boj_js_add_script' );
function boj_js_add_script() {
  wp_enqueue_script( $handle, $src, $dependencies, $ver, $in_footer );
}
```
### Adding a Core Script
This is equivalent to adding the following line to the document <head>:
```php
// Example 1: Add prototype.js which is bundled with WordPress
function boj_js_add_script1() {
  wp_enqueue_script( 'prototype' );
}
```
### Adding a Custom Script
To add a custom script to your code you need to specify its source as
well as its handle:
```php
// Example 2: Add a custom script
function boj_js_add_script2() {
  wp_enqueue_script( 'boj1', 'http://example.com/script1.js' );
}
```
### Adding a Custom Script with Dependencies
```php
// Example 3: Add a custom script that relies on jQuery components
function boj_js_add_script3() {
  wp_enqueue_script( 'boj2', 'http://example.com/script2.js',
    array( 'jquery-ui-tabs', 'jquery-ui-draggable' )
  );
}
```
Here you have specifi ed that the script depends on other scripts, which therefore need to be loaded
before. These scripts are included in WordPress, so their handle is enough information.
### Adding a Custom Script with a Version Number
Including version numbers with your scripts is often practical, and it is easy to accomplish.
```php
// Example 4: Add a custom script with version number
function boj_js_add_script4() {
  wp_enqueue_script( 'boj3', 'http://example.com/script3.js', '', '1.3.3.7' );
}
```
### Adding Scripts in the Footer
By default, wp_enqueue_script() will output the corresponding < script > tag within the < head >
of the resulting HTML document. Instead, you can elect to add it near the end of document with
passing true as a last parameter:
```php
// Example 5: Add a custom script in the footer
function boj_js_add_script5() {
  wp_enqueue_script( 'boj4', 'http://example.com/script4.js', '', '', true );
}
```
This adds the script near the closing </body> tag.

Injecting a script in the footer is possible if WordPress knows that it is currently
rendering the footer. In the admin area, this always works, but for the blog part
it requires the theme to use the `wp_footer()` function in its footer. Any good
theme should do this, but be warned that bad themes exist!
