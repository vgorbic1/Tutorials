##Menus and Submenus
###Top-Level Menu
A top-level menu is common practice for any plugin that needs multiple option pages. To register a top-level menu, you use the ```add_menu_page()``` function.
```php
add_menu_page( page_title, menu_title, capability, menu_slug, function, icon_url, position );
```
- page_title — The title of the page as shown in the 'title' tags
- menu_title — The name of your menu displayed on the dashboard
- capability — Minimum capability required to view the menu
- menu_slug — Slug name to refer to the menu; should be a unique name
- function : Function to be called to display the page content for the item
- icon_url — URL to a custom image to use as the Menu icon
- position — Location in the menu order where it should appear

To create a new menu for your plugin to see the menu process in action use the admin_menu action hook to trigger your menu code. This is the appropriate hook to use whenever you create menus and submenus in your plugins.
```
add_action( 'admin_menu', 'boj_menuexample_create_menu' );
function boj_menuexample_create_menu() {
  //create custom top-level menu
  add_menu_page( 'My Plugin Settings Page', 'Menu Example Settings', 'manage_options', __FILE__, 'boj_menuexample_settings_page', plugins_url( ‘/images/wp-icon.png’, __FILE__ ) );
}
```
Set the name of your menu to Menu Example Settings, which requires that the user has manage_options capabilities (that is, is an administrator).

###Submenu
To register a submenu, use the ```add_submenu_page()``` function.
```php
add_submenu_page( parent_slug, page_title, menu_title, capability, menu_slug, function );
```
- parent_slug : Slug name for the parent menu ( menu_slug previously defined)
- page_title : The title of the page as shown in the 'title' tags
- menu_title : The name of your submenu displayed on the dashboard
- capability : Minimum capability required to view the submenu
- menu_slug : Slug name to refer to the submenu; should be a unique name
- function : Function to be called to display the page content for the item
```php
add_action( 'admin_menu', 'boj_menuexample_create_menu' );
function boj_menuexample_create_menu() {
  //create custom top-level menu
  add_menu_page( 'My Plugin Settings Page', 'Menu Example Settings',
    'manage_options', __FILE__, 'boj_menuexample_settings_page',
    plugins_url( '/images/wp-icon.png', __FILE__ ) );
    
  //create submenu items
  add_submenu_page( __FILE__, 'About My Plugin', 'About', 'manage_options',
    __FILE__.'_about', boj_menuexample_about_page );
  add_submenu_page( __FILE__, 'Help with My Plugin', 'Help', 'manage_options',
    __FILE__.'_help', boj_menuexample_help_page );
  add_submenu_page( __FILE__, 'Uninstall My Plugin', 'Uninstall', 'manage_options', 
    __FILE__.'_uninstall', boj_menuexample_uninstall_page );
}
```
