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
The Plugin URI is a direct link to your plugin detail web page. The version number is the current version of the plugin. WordPress uses the version number set here to check for new plugin updates at WordPress.org. Below the plugin header comment block, it’s a good idea to include the license for your plugin. WordPress is licensed under the GNU General Public License (GPL) software license and as such
any plugin distributed for WordPress should be compatible with the GPL.
```
Copyright YEAR PLUGIN_AUTHOR_NAME (email : PLUGIN AUTHOR EMAIL)
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA
```
Place the license code just below your plugin header. By including this software license, your plugin will be licensed under the GPL.

####Plugin Paths
You shouldn’t hardcode directory paths in WordPress, but rather use the available functions to determine the correct path. To determine the local path to your plugin, you need to use the ```plugin_dir_path()``` function.
```php
echo plugin_dir_path( __FILE__ );
```
The parameter you send the function is the path to your file, using the __FILE__ constant. This is a PHP constant that always contains the absolute path to the file it is called from.

List of WordPress URL paths:
- plugins_url() — Full plugins directory URL (for example, http://example.com/wp-content/plugins )
- includes_url() — Full includes directory URL (for example, http://example.com/wp-includes )
- content_url() — Full content directory URL (for example, http://example.com/wp-content )
- admin_url() — Full admin URL (for example, http://example.com/wp-admin/ )
- site_url() — Site URL for the current site as set in wp_options table, which can be a subdomain (for example, http://example.com/wordpress )
- home_url() — Home URL for the current site, the addres you want people to visit to view your site (for example, http://example.com )

The ```plugins_url()``` function will be one of your best friends when building plugins in WordPress. This function can help you easily determine the full URL to any file within your plugin directory:
```
plugins_url( $path, $plugin ); 
// where $path - (string) (optional) — Path relative to the plugins URL
// and $plugin - (string) (optional) — Plugin file that you want to be relative (that is, pass in __FILE__ )
```
To reference an image fi le to use as an icon in your plugin:
```php
echo '< img src="' . plugins_url('images/icon.png', __FILE__ ) . '" > ';
// gives you <img src="http://example.com/wp-content/plugins/my-custom-plugin/images/icon.png">
```
Advantages of using  ```plugins_url():
- Supports the mu-plugins plugin directory.
- Auto detects SSL, so if SSL is enabled in WordPress, the URL returned would contain https.
- Uses the WP_PLUGIN_URL constant, meaning it can detect the location of the plugin even if the user has moved it to a custom location.
- Supports Multisite using the WPMU_PLUGIN_URL constant.

####Activation Function
The plugin activation function is triggered when a plugin is activated in WordPress. This function is called ```register_activation_hook()```. Using this function is a great way to set some default options for your plugin. It can also verify that the version of WordPress is compatible with your plugin.
```php
register_activation_hook( __FILE__, 'boj_myplugin_install' );

function boj_myplugin_install() {
  //do cool activation stuff
}
```
The second parameter is the unique function you want to call when your plugin is activated.

To the version of WordPress is compatible with your plugin:
```php
register_activation_hook( __FILE__, 'boj_install' );

function boj_install() {
  if ( version_compare( get_bloginfo( 'version' ), '3.1', '<' ) ) {
    deactivate_plugins( basename( __FILE__ ) ); // Deactivate our plugin
  }
}
```

#### Create Default Settings on Activate
Rather than forcing the user to visit your settings page and set those options, you can automatically set default options when the
plugin is activated.
```php
register_activation_hook( __FILE__, 'boj_install' );
function boj_install() {
  $boj_myplugin_options = array(
    'view' = > 'grid',
    'food' = > 'bacon',
    'mode' = > 'zombie'
  );
  update_option( 'boj_myplugin_options', $boj_myplugin_options );
}
```

####Plugin Deactivation
The ```register_deactivation_hook()``` function is triggered when your plugin is deactivated in the WordPress Plugins screen. This function accepts the same two parameters as the previous activation function:
```php
register_deactivation_hook( __FILE__, 'boj_myplugin_uninstall' );
function boj_myplugin_uninstall() {
  //do something
}
```
When dealing with the deactivation function, you shouldn’t include uninstall functionality when a plugin is deactivated. The WordPress automatic update feature deactivates all plugins prior to installing the new version of WordPress.

####Uninstall Plugin
WordPress provides two different methods for uninstalling a plugin: the uninstall.php file and the uninstall hook. The first one is typically the preferred method because it keeps all your uninstall code in a separate file. To use this method, create an uninstall.php file and place it in the root directory of your plugin. If this file exists WordPress executes its contents when
the plugin is deleted from the WordPress Plugins screen page:
```php
// Check if uninstall not called from WordPress. If not, 
// WP_UNINSTALL_PLUGIN should exist.
if ( !defined( 'WP_UNINSTALL_PLUGIN' ) )
exit ();
// Delete option from options table
delete_option( 'boj_myplugin_options' );
//remove any additional options and custom tables
```
The goal of a plugin uninstall script is to remove any trace of the plugin from the WordPress database, including deleting all options and dropping any custom tables that may have been created. You don’t need to worry about deleting the actual plugin files or directories in this function. WordPress will do that for you once your uninstall script runs.

If you delete a plugin in WordPress and uninstall.php does not exist, WordPress executes the uninstall hook (if it exists). 
```php
register_activation_hook( __FILE__, 'boj_myplugin_activate' );

function boj_myplugin_activate() {
  //register the uninstall function
  register_uninstall_hook( __FILE__, 'boj_myplugin_uninstaller' );
}
  
function boj_myplugin_uninstaller() {
  //delete any options, tables, etc the plugin created
  delete_option( 'boj_myplugin_options' );
}
```
The ```register_uninstall_hook()``` should be called on activation and not on every plugin load. To do this you’ll include the uninstall hook when the plugin is activated using the ```register_activation_hook()```. Remember if the uninstall.php file exists in your plugins root folder, the uninstall hook won’t actually execute. It’s a much cleaner, and easier, process to use the uninstall.php method described earlier for removing plugin settings and options when a plugin is deleted in WordPress.
