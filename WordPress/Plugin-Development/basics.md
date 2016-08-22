##Basics
It’s highly recommended to store all your plugin files inside a folder within the plugins directory in WordPress. The folder name should be the same as the main plugin filename. You shouldn’t include any spaces or underscores in the folder name; instead use hyphens if needed. 

####Prefix Everything
When building a custom plugin, it’s essential that you prefix everything with a unique prefix. This means all plugins files, function names, variable names, and everything included with your plugin. One of the most common errors in plugins is using all too common names for function and variables. A good rule of thumb is to prefi x everything with your plugin initials and your own initials. For instance if your name is Michael Myers and your plugin is named Halloween Revenge, you would prefix the function as ```mm_hr_update_options()```.
Don’t use general names when creating variables. You can use the same prefix method previously described and name your variable  ```$mm_hr_post```.

####File Organization
You should have only two files in your plugin folder: the primary plugin PHP file and your uninstall.php file. For organizational reasons, store all other plugin files in a subdirectory. You should group all admin interface functions in a separate file. This allows you to conditionally include the admin code only when the user is viewing the admin side of WordPress:
```php
<?php
if ( is_admin() ) {
  // we’re in wp-admin
  require_once( dirname(__FILE__).'/includes/admin.php' );
}
?>
```

####Folder Structure
If your plugin requires JavaScript files, create a ```/js``` folder and store all the JavaScript files in this directory. If you have custom style sheet files, create a ```/css``` folder to store all your CSS files. Keep all images stored in a ```/images``` folder:

![wp-plugin-folder-structure](https://cloud.githubusercontent.com/assets/13823751/17871184/1d5ae590-6880-11e6-915d-7fd4ca3f5c20.jpg)

####Header Requirements
The plugin header is the only requirement for a plugin to function in WordPress:
```php
<?php
/*
Plugin Name: My Plugin
Plugin URI: http://example.com/wordpress-plugins/my-plugin
Description: A brief description of my plugin
Version: 1.0
Author: Brad Williams
Author URI: http://example.com
License: GPLv2
*/
? >
```
The Plugin URI is a direct link to your plugin detail web page. The version number is the current version of the plugin. WordPress uses the version number set here to check for new plugin updates at WordPress.org.
