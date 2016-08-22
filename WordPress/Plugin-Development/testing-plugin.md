##Testing Plugin Functionality
On occasion you may want to test some plugin functionality without actually creating a plugin to do so. Make a test.php file with the following code snippet and place it in your WordPress root directory:
```php
<?php
// Load the WordPress Environment
// define( ‘WP_DEBUG’, true ); /* uncomment for debug mode */
require(‘./wp-load.php’);
// require_once (‘./wp-admin/admin.php’); /* uncomment for is_admin() */
?>
<pre>
<?php
/* test stuff here */
var_dump( is_admin() );
?>
</pre>
```
Once you have included the required WordPress core fi les, you want test any code that would otherwise exist reside in your plugin. Don ’ t forget to remove your test.php fi le when you are done testing.
