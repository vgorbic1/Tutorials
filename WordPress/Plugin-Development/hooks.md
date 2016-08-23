##Hooks
Hooks are the backbone of WordPress. They enable plugin developers to “hook” into the WordPress workflow to change how it works without directly modifying the core code. This enables users to easily upgrade to newer versions of WordPress without losing modifications. 
WordPress has two primary types of hooks: action hooks and filter hooks. The former enables you to execute a function at a certain point, and the latter enables you to manipulate the output passed through the hook. Hooks aren’t just for plugins. WordPress uses hooks internally.

###Actions
Action hooks enable you to fire a function at specific points in the WordPress loading process or when an event occurs. For example, you might want a function to execute when WordPress first loads a page or when a blog post is saved. An action is technically a PHP function. For a function to be considered an action, it would need to be registered for an action hook. Hooks might be fired more than once in the WordPress flow for various reasons. Any actions added to these hooks will execute each time the hook is fired.

####do_action()
When hooking into WordPress, your plugin won’t call this function directly; however, your plugin will almost always use it indirectly.
```php
  do_action( $tag, $arg = '' );
```
- $tag — The name of the action hook.
- $arg — Value(s) passed to registered actions. Action hooks have the option to pass any number of parameters or no parameters at all. You need to check the WordPress source code for specific hooks because the number of parameters changes on a per-hook basis. 

```wp_head``` hook is fired within the <head> area on the front end of the site. WordPress and plugins usually use this hook to add meta information, style sheets, and scripts.
```php
do_action( 'wp_head' );
```
When this code fires in WordPress, it looks for any actions registered for the ```wp_head``` action hook. It then executes them in the order specified. As you can see, it has a name of ```wp_head``` but passes no extra parameters. This is often the case with action hooks.

####add_action()
You develop custom functions (actions) that perform a specific task when the action hook is fi red. To do this, you would use the ```add_action()``` function.
```php
add_action( $tag, $function, $priority, $accepted_args );
```
- $tag — The name of the action hook your function executes on.
- $function — The name of your function that WordPress calls.
- $priority — An integer that represents the order in which the action is fired. When no value is given, it defaults to 10. The lower the number, the earlier the function will be called. The higher the number, the later it will be called.
- $accepted_args — The number of parameters the action hook will pass to your function. By default, it passes only one parameter.

Your plugin can add multiple functions to an action hook. Other plugins, and even WordPress core, often add functions to the same hook.
One common action hook is ```wp_footer```. It is fired on the front end of the site by the user’s WordPress theme. Generally, it is fired just before the closing </body> tag in the HTML.
```php
add_action('wp_footer', 'boj_example_footer_message', 100 );
function boj_example_footer_message() {
  echo 'This site is built using <a href="http://wordpress.org" title="WordPress publishing platform">WordPress</a>.';
}
```

####do_action_ref_array()
The ```do_action_ref_array()``` function works the same way as ```do_action()``` works, with a difference in how the arguments are passed. Rather than passing multiple, optional values as additional parameters, it passes an array of arguments. The array of arguments is also a required parameter. The purpose of the function is to pass an object by reference to actions added to a specific hook. This means the action can change the object itself without returning it.

The following code shows the pre_get_posts action hook. WordPress executes this hook before loading posts from the database, enabling plugins to change how posts are queried.
```php
do_action_ref_array('pre_get_posts', array( &$this ));
```
The second parameter in this case is an array of query arguments for pulling posts from the database. This hook enables you to execute code based on that array of arguments.

To randomly order posts on the blog home page rather than have the default ordering by the post date. You would register an action on this hook and change the order.
```php
add_action( 'pre_get_posts', 'boj_randomly_order_blog_posts' );
function boj_randomly_order_blog_posts( $query ) {
  if ( $query->is_home && empty( $query->query_vars['suppress_filters'] ) )
    $query-> set( 'orderby', 'rand' );
}
```

####remove_action()
```remove_action()``` enables you to remove an action that has previously been added to a hook. Typically, you would remove actions that WordPress adds by default. To remove an action, the action must have already been added using the ```add_action()``` function. If your code runs before the action is registered, the action will not be removed from the hook. The function returns true when the action was successfully removed and false when the action could not be removed.
```php
remove_action( $tag, $function_to_remove, $priority, $accepted_args );
```
- $tag — The name of the action hook the action you want to remove is hooked to.
- $function_to_remove — The name of the function that has been added to the hook.
- $priority — The priority given in the ```add_action()``` function. This defaults to a value of 10.
- $accepted_args — The number of accepted arguments the action accepts. This defaults to a value of 1.

Generally, you remove actions within WordPress. Many of its default actions are defined in the wp-includes/default-filters.php file.

####remove_all_actions()
In some plugins, you may find it necessary to remove all actions for a given tag or all actions for a given tag and priority. The ```remove_all_actions()``` function enables you to do this with a single line of code instead of multiple uses of the ```remove_action()``` function.

To remove all actions, regardless of priority, from the ```wp_head``` action hook.
```php
remove_all_actions('wp_head');
```
To remove all actions with a priority of 1 for the ```wp_head``` hook:
```php
remove_all_actions( 'wp_head', 1 );
```
You should be careful when using this function. Other plugins and themes may add actions that you are unaware of. Using this may break functionality that your plugin users are expecting to work. It’s usually better to be as specific as possible with your code. In most cases, you should use the ```remove_action()``` function instead.

####has_action()
Sometimes, you may find it necessary to check if a hook has any actions or if a specific action has been added to a hook before executing code. The ```has_action()``` function is a conditional function that gives you the ability to check both these cases.
```php
has_action( $tag, $function_to_check );
```
- $tag — The name of the action hook you want to check for actions registered to it.
- $function_to_check — The name of a function to check if it has been added to the hook. This parameter is optional and defaults to a value of false.

If ```$function_to_check``` is not set, the function returns true if actions are added to the hook or false if no actions are added to the hook. If ```$function_to_check``` is set and the function has been added to the hook, the priority (integer) of the action will be returned. Otherwise, a value of false will be returned.

To display a message based on whether the ```wp_footer``` action hook has any action registered for it.
```php
if ( has_action( 'wp_footer' ) ) {
  echo '<p>An action has been registered for the footer.</p>';
} else {
  echo '<p>An action hasn\'t been registered for the footer.</p >';
}
```

####did_action()
The ```did_action()``` function enables your plugin to check if an action hook has already been executed or to count the number of times one has been executed. This also means that some action hooks are fired multiple times during a single page load. The function returns the number of times the hook has been fired or false if it hasn’t been fired. The most common use case of the function is to check if an action hook has already been fired and execute code based on the return value of ```did_action()```.

To define a PHP constant if the ```plugins_loaded``` action hook has already fired:
```php
if ( did_action( 'plugins_loaded' ) ) {
  define( 'BOJ_MYPLUGIN_READY', true );
}
```
####register_activation_hook() and register_deactivation_hook()
WordPress has two functions for registering action hooks for the activation and deactivation of individual plugins. These are technically functions to create custom hooks.

###Commonly Used Action Hooks
####plugins_loaded
For plugin developers, the plugins_loaded action hook is probably the most important hook. It is fired after most of the WordPress files are loaded but before the pluggable functions and WordPress starts executing anything. In most plugins, no other code should be run until this hook is fired. ```plugins_loaded``` is executed when all the user's activated plugins have been loaded by WordPress. It
is also the earliest hook plugin developers can use in the loading process.
```php
add_action('plugins_loaded', 'boj_footer_message_plugin_setup');
function boj_footer_message_plugin_setup() {
  /* Add the footer message action. */
  add_action('wp_footer', 'boj_example_footer_message', 100);
}
function boj_example_footer_message() {
  echo 'This site is built using <a href="http://wordpress.org" title="WordPress publishing platform">WordPress</a>.';
}
```

####init
The ```init``` hook is fi red after most of WordPress is set up. WordPress also adds a lot of internal functionality to this hook such as the registration of post types and taxonomies and the initialization of the default widgets. Because nearly everything in WordPress is ready at this point, your plugin will probably use this hook for anything it needs to do when all the information from WordPress is available.

To add the ability for users to write an excerpt for pages. You would do this on init because the "page" post type is created at this point using the ```add_post_type_support()``` function:
```php
add_action('init', 'boj_add_excerpts_to_pages');
function boj_add_excerpts_to_pages() {
  add_post_type_support('page', array('excerpt'));
}
```

####admin_menu
The ```admin_menu hook``` is called only when an administration page loads. Whenever your plugin works directly in the admin, you would use this hook to execute your code.

To add a sub-menu item labeled BOJ Settings to the Settings menu in the WordPress admin:
```php
add_action('admin_menu', 'boj_admin_settings_page');
function boj_admin_settings_page() {
  add_options_page(
    'BOJ Settings',
    'BOJ Settings',
    'manage_options',
    'boj_admin_settings',
    'boj_admin_settings_page'
  );
}
```

####template_redirect 
The ```template_redirect``` action hook is important because it’s the point where WordPress knows which page a user is viewing. It is executed just before the theme template is chosen for the particular page view. It is fi red only on the front end of the site and not in the administration area. This is a good hook to use when you need to load code only for specific page views.
```php
add_action('template_redirect', 'boj_singular_post_css');
function boj_singular_post_css() {
  if ( is_singular('post') ) {
    wp_enqueue_style('boj-singular-post', 'boj-example.css', false, 0.1, 'screen');
  }
}
```

####wp_head
On the front end of the site, WordPress themes call the ```wp_head()``` function, which fires the ```wp_head``` hook. Plugins use this hook to add HTML between the opening <head> tag and its closing </head>.

To add a meta description on the front page of the site using the site's description:
```php
add_action('wp_head', 'boj_front_page_meta_description' );
function boj_front_page_meta_description() {
  /* Get the site description. */
  $description = esc_attr( get_bloginfo('description') );
  /* If a description is set, display the meta element. */
  if ( !empty( $description ) ) {
    echo '<meta name="description" content="' . $description . '" /> ';
  }
}
```
Many plugins incorrectly use the wp_head action hook to add JavaScript to the header when they should be using the ```wp_enqueue_script()``` function. The only time JavaScript should be added to this hook is when it's not located in a separate JavaScript file.

##Filters
