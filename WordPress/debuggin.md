## Debugging Techniques
In your WordPress install, open the `wp-config.php` file, which is at the root of the install by
default. The `wp-config.php` file will have a line that looks like this:
```
define('WP_DEBUG', false);
```
What this line does is tell WordPress that debug mode should be disabled, so no debug messages should
be shown. You don’t want debugging disabled on your development install. You need to enable it.
To turn debugging on, change false to true. Enabling debugging makes two important things possible for debugging your plugins:
- Displays debug messages directly on the screen as they happen. This is the default behavior
when WP_DEBUG is set to true.
- Enables you to use the error logging feature of WordPress.

If you’re running any other plugins, you’ll most likely see numerous error messages displayed in various places on the page. This is
because most plugins aren’t coded to the standards they should be. You have the advantage of this
chapter, so there’s no excuse for any of your plugins to be displaying debug errors.

WordPress offers another useful tool for debugging your site: error logging. This feature is an
extension of the debugging process previously described. It creates an error log file that keeps track
of issues as they happen on your WordPress installation. Error log messages
are saved in a debug.log file within the WordPress install’s `wp-content` directory by default.

To enable error logging, you need to edit your WordPress install’s `wp-config.php` file:
```
define( 'WP_DEBUG_LOG', true );
```
You can also optionally disable the display of debug messages on the site and save them only in the
debug file. This is a useful technique if you want to keep track of debug messages on a live site rather
than a development install. To do this, you need to add two new lines to your `wp-config.php` file.
```
define( 'WP_DEBUG_DISPLAY', false );
ini_set( 'display_errors', 0 );
```
After enabling error logging, you may optionally add the following line to change the path and filename:
```
ini_set( 'error_log', '/example/example.com/wp-content/logs/debug.log' );
```
