##Testing Plugin Functionality
On occasion you may want to test some plugin functionality without actually creating a plugin to do so. Make a test.php fi le with the following code snippet and place
it in your WordPress root directory:
```php
< ?php
// Load the WordPress Environment
// define( ‘WP_DEBUG’, true ); /* uncomment for debug mode */
require(‘./wp-load.php’);
// require_once (‘./wp-admin/admin.php’); /* uncomment for is_admin() */
? >
< pre >
< ?php
/* test stuff here */
var_dump( is_admin() );
? >
< /pre >
```
