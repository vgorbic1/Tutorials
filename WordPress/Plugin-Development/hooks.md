## Hooks
Hooks are the backbone of WordPress. They enable plugin developers to “hook” into the WordPress workflow to change how it works without directly modifying the core code. This enables users to easily upgrade to newer versions of WordPress without losing modifications. 

New hooks are always added with new versions of WordPress. Keeping track of changes in the core code from version to version can help you stay on top of new hooks that you can use within your plugins. There's no better process for understanding how PHP code works than actually looking at the code and following each statement made within the code. An easy way to search for hooks is to open a file from the wordpress folder in your preferred text editor and run a text search for one of four function names.
- do_action
- do_action_ref_array
- apply_filters
- apply_filters_ref_array

WordPress has two primary types of hooks: action hooks and filter hooks. The former enables you to execute a function at a certain point, and the latter enables you to manipulate the output passed through the hook. Hooks aren’t just for plugins. WordPress uses hooks internally.

### Actions
Action hooks enable you to fire a function at specific points in the WordPress loading process or when an event occurs. For example, you might want a function to execute when WordPress first loads a page or when a blog post is saved. An action is technically a PHP function. For a function to be considered an action, it would need to be registered for an action hook. Hooks might be fired more than once in the WordPress flow for various reasons. Any actions added to these hooks will execute each time the hook is fired.

#### do_action()
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

#### add_action()
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

#### do_action_ref_array()
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

#### remove_action()
`remove_action()` enables you to remove an action that has previously been added to a hook. Typically, you would remove actions that WordPress adds by default. To remove an action, the action must have already been added using the ```add_action()``` function. If your code runs before the action is registered, the action will not be removed from the hook. The function returns true when the action was successfully removed and false when the action could not be removed.
```php
remove_action( $tag, $function_to_remove, $priority, $accepted_args );
```
- $tag — The name of the action hook the action you want to remove is hooked to.
- $function_to_remove — The name of the function that has been added to the hook.
- $priority — The priority given in the ```add_action()``` function. This defaults to a value of 10.
- $accepted_args — The number of accepted arguments the action accepts. This defaults to a value of 1.

Generally, you remove actions within WordPress. Many of its default actions are defined in the wp-includes/default-filters.php file.

#### remove_all_actions()
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

#### has_action()
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

#### did_action()
The ```did_action()``` function enables your plugin to check if an action hook has already been executed or to count the number of times one has been executed. This also means that some action hooks are fired multiple times during a single page load. The function returns the number of times the hook has been fired or false if it hasn’t been fired. The most common use case of the function is to check if an action hook has already been fired and execute code based on the return value of ```did_action()```.

To define a PHP constant if the ```plugins_loaded``` action hook has already fired:
```php
if ( did_action( 'plugins_loaded' ) ) {
  define( 'BOJ_MYPLUGIN_READY', true );
}
```
#### register_activation_hook() and register_deactivation_hook()
WordPress has two functions for registering action hooks for the activation and deactivation of individual plugins. These are technically functions to create custom hooks.

### Commonly Used Action Hooks
#### plugins_loaded
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

#### init
The ```init``` hook is fi red after most of WordPress is set up. WordPress also adds a lot of internal functionality to this hook such as the registration of post types and taxonomies and the initialization of the default widgets. Because nearly everything in WordPress is ready at this point, your plugin will probably use this hook for anything it needs to do when all the information from WordPress is available.

To add the ability for users to write an excerpt for pages. You would do this on init because the "page" post type is created at this point using the ```add_post_type_support()``` function:
```php
add_action('init', 'boj_add_excerpts_to_pages');
function boj_add_excerpts_to_pages() {
  add_post_type_support('page', array('excerpt'));
}
```

#### admin_menu
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

#### template_redirect 
The ```template_redirect``` action hook is important because it’s the point where WordPress knows which page a user is viewing. It is executed just before the theme template is chosen for the particular page view. It is fi red only on the front end of the site and not in the administration area. This is a good hook to use when you need to load code only for specific page views.
```php
add_action('template_redirect', 'boj_singular_post_css');
function boj_singular_post_css() {
  if ( is_singular('post') ) {
    wp_enqueue_style('boj-singular-post', 'boj-example.css', false, 0.1, 'screen');
  }
}
```

#### wp_head
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

### Filters
Filter hooks enable you to manipulate the output of code. Whereas action hooks enable you to insert code, filter hooks enable you to overwrite code that WordPress passes through the hook. Your function would “filter” the output. 

A filter is a function registered for a filter hook. The function itself would take in at least a single parameter and return that parameter after executing its code. Without a filter, filter hooks don’t do anything. They exist so that plugin developers can change different variables. This can be anything from a simple text string to a multidimensional array.

You can add multiple filters to the same filter hook. Other plugins and WordPress can also add filters to the hook. Filter hooks aren’t limited to a single filter. It is important to note this because each filter must always return a value for use by the other filters. If your function doesn’t return a value, you risk breaking the functionality of both WordPress and other plugins.

#### apply_filters()
```php
apply_filters($tag, $value);
```
- $tag — The name of the filter hook.
- $value — The parameter passed to any filters added to the hook. The function can also take in any number of extra $value parameters to pass to filters. It must be returned back to WordPress when writing a filter.
```php
apply_filters('template_include', $template);
```
In this example, ```template_include``` is name of the filter hook. ```$template``` is a file name that can be changed through filters registered for the filter hook.
```php
add_filter('wp_title', 'boj_add_site_name_to_title', 10, 2 );
function boj_add_site_name_to_title($title, $sep) {
  /* Get the site name. */
  $name = get_bloginfo('name');
  /* Append the name to the $title variable. */
  $title .= $sep . ' ' . $name;
  /* Return the title. */
  return $title;
}
```
#### add_filter()
To add a filter, use the ```add_filter()``` function.
```php
add_filter($tag, $function, $priority, $accepted_args);
```
- $tag — The name of the hook you want to register your filter for.
- $function — The function name of the filter that you create to manipulate the output.
- $priority — An integer that represents in what order your filter should be applied. If no value is added, it defaults to 10.
- $accepted_args — The number of parameters your filter function can accept. By default this is 1 . Your function must accept at least one parameter, which will be returned.

#### apply_filters_ref_array()
The ```apply_filters_ref_array()``` function works nearly the same as ```apply_filters()```. One major difference is what parameters are passed. Rather than accepting multiple values, it accepts an array of arguments. Both parameters are required. It is also important to note that the ```$args``` parameter should be passed by reference rather than value.

#### remove_filter()
The ```remove_filter()``` function enables plugins to remove filters that have been previously registered for a fi lter hook. To successfully remove a filter, this function must be called after a filter has been registered using the ```add_filter()``` function.
```php
remove_filter( $tag, $function_to_remove, $priority, $accepted_args );
```
- $tag — The name of the filter hook to remove a filter from.
- $function_to_remove — The function to remove from the filter hook.
- $priority — The priority previously used in add_filter() to register the filter. This parameter defaults to 10.
- $accepted_args — The number of accepted arguments previously declared in the add_filter() called to register the filter. This parameter defaults to 1 .

The function returns true when the filter is successfully removed and returns false when the removal is unsuccessful. The $tag, $function_to_remove, and $priority parameters must also match the parameters set with add_filter() exactly. Otherwise, the filter will not be removed.
```php
remove_filter('the_content', 'wpautop');
```

#### remove_all_filters()
In some plugins, you may need to remove all filters from a specifi c filter hook or remove filters with a particular priority from a filter hook. The ```remove_all_filters()``` function enables you to do this with a single line of code.
```php
remove_all_filters('the_content', 11);
```

#### has_filter()
The ```has_filter()``` function enables plugins to check if any filters have been registered for a filter hook or if a specifi c filter has been registered for the hook.
```php
has_filter( $tag, $function_to_check );
```
The function returns false if no filter is found for the given hook. It returns true if a filter is found. However, if the ```$function_to_check``` parameter is set, it returns the priority of the filter.
```php
if ( has_filter( 'the_content', 'wpautop' ) ) echo 'Paragraphs are automatically formatted for the content.';
```

#### current_filter()
The ```current_filter()``` function returns the name of the fi lter hook currently executed. However, it doesn’t just work with filter hooks; it applies to action hooks as well, so it returns the name of the current action or fi lter hook. This function is especially useful if you use a single function for multiple hooks but need the function to execute differently depending on the hook currently firing.

To set an array of unwanted words depending on the case and replace them with “Whoops!” in the text.
```php
add_filter('the_content', 'boj_replace_unwanted_words');
add_filter('the_title', 'boj_replace_unwanted_words');
function boj_replace_unwanted_words($text) {
  /* If the_content is the filter hook, set its unwanted words. */
  if ('the_content' == current_filter() ) {
    $words = array('profanity', 'curse', 'devil');
    /* If the_title is the filter hook, set its unwanted words. */
  } elseif ('the_title' == current_filter() ) {
    $words = array( ‘profanity’, ‘curse’ );
    /* Replace unwanted words with “Whoops!” */
    $text = str_replace($words, 'Whoops!', $text);
  }
  /* Return the formatted text. */
  return $text;
}
```

### WordPress functions for quickly returning values
- __return_false — Returns the Boolean value of false.
- __return_true — Returns the Boolean value of true.
- __return_empty_array — Returns an empty PHP array.
- __return_zero — Returns the integer 0.

### Commonly Used Filter Hooks
#### the_content
If there’s one filter hook that plugin authors use more than any other, it is the_content. Without content, a site would be essentially useless. It is the most important thing displayed on the site, and plugins use this hook to add many features to a site.

To append a list of related posts by post category to the_content for a reader to see when viewing a single post.
```php
add_filter('the_content', 'boj_add_related_posts_to_content');
function boj_add_related_posts_to_content($content) {
  /* If not viewing a singular post, just return the content. */
  if ( !is_singular('post') ) {
    return $content;
  }
  /* Get the categories of current post. */
  $terms = get_the_terms( get_the_ID(), ‘category’ );
  /* Loop through the categories and put their IDs in an array. */
  $categories = array();
  foreach ( $terms as $term ) {
    $categories[] = $term- > term_id;
    /* Query posts with the same categories from the database. */
    $loop = new WP_Query(array(
      ‘cat__in’ = > $categories,
      ‘posts_per_page’ = > 5,
      ‘post__not_in’ = > array( get_the_ID() ),
      ‘orderby’ = > ‘rand’
    ));
    
    /* Check if any related posts exist. */
    if ( $loop- > have_posts() ) {
      /* Open the unordered list. */
      $content .= ‘ < ul class=”related-posts” > ’;
      while ( $loop- > have_posts() ) {
        $loop- > the_post();
        /* Add the post title with a link to the post. */
        $content .= the_title(‘ < li > < a href=”’ . get_permalink() . ‘” > ’, ‘ < /a > < /li > ’, false);
    }
    /* Close the unordered list. */
    $content .= ‘ < /ul > ’;
    /* Reset the query. */
    wp_reset_query();
  }
  /* Return the content. */
  return $content;
}
```

#### the_title
To strip all tags a user might use when writing a post title:
```php
add_filter('the_title', 'boj_strip_tags_from_titles');
function boj_strip_tags_from_titles( $title ) {
  $title = strip_tags( $title );
  return $title;
}
```

#### comment_text
The ```comment_text``` hook is often a useful fi lter hook because comments typically play a large role for blogs and other types of sites.
```php
add_filter('comment_text', 'boj_add_role_to_comment_text');
function boj_add_role_to_comment_text( $text ) {
  global $comment;
  /* Check if comment was made by a registered user. */
  if ( $comment-> user_id > 0 ) {
  /* Create new user object. */
  $user = new WP_User( $comment-> user_id );
  /* If user has a role, add it to the comment text. */
    if ( is_array( $user- > roles ) ) {
      $text .= ‘ < p > User Role: ‘ . $user- > roles[0] . ‘ < /p > ’;
    }
  }
return $text;
}
```
#### template_include
```template_include``` is a sort of catchall filter hook for many other, more specific filter hooks. It is used after the theme template file for the current page has been chosen. WordPress chooses a template based on the page currently viewed by a reader. You can add a filter for each of the individual filter hooks or filter them all at the end with the ```template_include``` hook.
- front_page_template
- home_template
- single_template
- page_template
- attachment_template
- archive_template
- category_template
- tag_template
- author_template
- date_template
- archive_template
- search_template
- 404_template
- index_template

### Hooks and Classes
Adding a method of a class as an action or filter, the format of the calls to ```add_action()``` and ```add_filter()``` is slightly different.
When using a method such as ```$function_to_add``` from within a class, you must change ```$function_to_add``` to an array with & $this as the fi rst argument and the method name as the second argument.
```php
add_action( $tag, array( & $this, $method_to_add ) );
```
When using a class method as a filter, you must also change the ```$function_to_add``` parameter.
```php
add_filter( $tag, array( & $this, $method_to_add ) );
```
For example, the ```add_filters()``` method checks if the reader is currently viewing a singular post view. If true, the ```content()``` method appends the last modifi ed date of the post to the post content.
```php
class BOJ_My_Plugin_Loader {
  /* Constructor method for the class. */
  function BOJ_My_Plugin_Loader() {
    /* Add the ‘singular_check’ method to the ‘template_redirect’ hook. */
    add_action( ‘template_redirect’, array( & $this, ‘singular_check’ ) );
  }
  /* Method used as an action. */
  function singular_check() {
    /* If viewing a singular post, filter the content. */
    if ( is_singular() ) add_filter( ‘the_content’, array( & $this, ‘content’ ) );
  }
  /* Method used as a filter. */
  function content( $content ) {
    /* Get the date the post was last modified. */
    $date = get_the_modified_time( get_option( ‘date_format’ ) );
    /* Append the post modified date to the content. */
    $content .= ‘ < p > Post last modified: ‘ . $date . ‘ < /p > ’;
    /* Return the content. */
    return $content;
  }
}
$boj_myplugin_loader = new BOJ_My_Plugin_Loader();
```

### Creating Custom Hooks
Plugins but they can also create custom hooks for use by other plugins and themes. Your plugin would use one of four available functions for creating custom action hooks:
- do_action()
- do_action_ref_array()
- apply_filters()
- apply_filters_ref_array()

Custom hooks make your plugin more flexible, allow it to be extended by others, and gives you the ability to hook into the execution of various processes throughout your plugin within the plugin itself. Using custom hooks also keep users from editing your work directly. The importance of this is that when you provide an update for the plugin, users won't lose any modifications they've made.

For example, you create a plugin setup function. The function defines a constant that can be altered. Other plugins may also execute any code they want on the hook. You provide it so that they have an opportunity to run code at that point.
```php
add_action( ‘plugins_loaded’, ‘boj_myplugin_setup’ );
function boj_myplugin_setup() {
  /* Allow actions to fire before anything else. */
  do_action( ‘boj_myplugin_setup_pre’ );
  /* Check if the root slug is defined. */
  if ( !defined( ‘BOJ_MYPLUGIN_ROOT_SLUG’ ) ) define( ‘BOJ_MYPLUGIN_ROOT_SLUG’, ‘articles’ );
}
```

### Variable Hooks
Variable hook names change based on a specific variable.
```php
do_action( "load-$pagenow" );
```
The $pagenow variable will become the page name being viewed. For example, the hook for the new post page in the admin would be load - post - new.php and the hook on the edit posts screen would be load - post.php . This enables plugins to run code only for specific page views in the admin.

