## Frontend User Registration
We can make use of the existing functionalities to implement registration
from the frontend. We can use a regular HTTP request or AJAX-based technique
to implement this feature.

#### Shortcode implementation
Shortcodes are the quickest way to add dynamic content to your pages. In this
situation, we need to create a page for registration. Therefore, we need to create a
shortcode that generates the registration form, as shown in the following code:
```php
add_shortcode( "register_form", "display_register_form" );
function display_register_form(){
  $html = "HTML for registration form";
  return $html;
}
```
Then, you can add the shortcode inside the created page using the following code
snippet to display the registration form:
```
[register_form]
```
Shortcodes are easy to implement in any part of your application, but it's hard to manage 
the template code assigned using the PHP variables, and there is a possibility of the 
shortcode getting deleted from the page by mistake.

#### Page template implementation
Page templates are a widely used technique in modern WordPress themes. We can
create a page template to embed the registration form:
```
/*
* Template Name : Registration
*/
HTML code for registration form
```
Next, we have to copy the template inside the theme folder. Finally, we can create
a page and assign the page template to display the registration form. A page template is more stable
than shortcode. Generally, page templates are associated with the look of the website rather
than providing dynamic forms. The full width page, two-column page, and
left sidebar page are some common implementations of page templates. A template is managed separately 
from logic, without using PHP variables. The page templates depend on the theme and need to be updated on
theme switching.

## Building a simple router for a user module
Routing is one of the important aspects in advanced application development.
We need to figure out ways of building custom routes for specific functionalities.
In this scenario, we will create a custom router to handle all the user-related
functionalities of our application:
- All the user-related functionalities should go through a custom URL,
such as http://www.example.com/user
- Registration should be implemented at http://www.example.com/user/
register
- Login should be implemented at http://www.example.com/user/login
- Activation should be implemented at http://www.example.com/user/
activate

Make sure to set up your permalinks structure to post name. If you prefer a different permalinks structure,
you will have to update the URLs and routing rules accordingly.

In MVC terms,
user acts as the controller and the next URL segment (register, login, and
activate) acts as the action.

#### Creating the routing rules
There are various ways and action hooks used to create custom rewrite rules.
We will choose the `init` action to define our custom routes for the user section:
```php
public function manage_user_routes() {
  add_rewrite_rule( '^user/([^/]+)/?',
  'index.php?control_action=$matches[1]', 'top' );
}
```
Based on the discussed requirements, all the URLs for the user section will follow
the `/user/custom action` pattern. Therefore, we will define the regular expression
for matching all the routes in the user section. Redirection is made to the index.php
file with a query variable called control_action. This variable will contain the URL
segment after the `/user` segment. The third parameter of the `add_rewrite_rule`
function will decide whether to check this rewrite rule before the existing rules or
after them. The value of top will give a higher precedence, while the value of bottom
will give a lower precedence.

We need to complete two other tasks to get these rewriting rules to take effect:
1. Add query variables to the WordPress `query_vars`
2. Flush the rewriting rules

#### Adding query variables
WordPress doesn't allow you to use any type of variable in the query string. It
will check for query variables within the existing list and all other variables will
be ignored. Whenever we want to use a new query variable, make sure to add it
to the existing list. First, we need to update our constructor with the following
filter to customize query variables:
```php
add_filter( 'query_vars', array( $this, 'manage_user_routes_query_vars' ) );
```
This filter on `query_vars` will allow us to customize the list of existing variables
by adding or removing entries from an array. Now, consider the implementation
to add a new query variable:
```php
public function manage_user_routes_query_vars( $query_vars ) {
  $query_vars[] = 'control_action';
  return $query_vars;
}
```
As this is a filter, the existing `query_vars` variable will be passed as an array. We
will modify the array by adding a new query variable called `control_action` and
return the list. Now, we have the ability to access this variable from the URL.

#### Flushing the rewriting rules
Once rewrite rules are modified, it's a must to flush the rules in order to prevent 404
page generation. Flushing existing rules is a time consuming task, which impacts the
performance of the application and hence should be avoided in repetitive actions
such as `init`. It's recommended that you perform such tasks in plugin activation or
installation as we did earlier in user roles and capabilities. So, let's implement the
function for flushing rewrite rules on plugin activation:
```
public function flush_application_rewrite_rules() {
  $this->manage_user_routes();
  flush_rewrite_rules();
}
```
As usual, we need to update the constructor to include the following action to
call the flush_application_rewrite_rules function:
```
register_activation_hook( __FILE__, array( $this, 'flush_application_rewrite_rules' ) );
```
You can get 404 errors due to the modification in rewriting rules and
not flushing it properly. In such situations, go to the Permalinks section
on the Settings page and click on the Save Changes button to flush the
rewrite rules manually.

Use the free plugin [Rewrite Rules Inspector](http://wordpress.org/plugins/rewrite-rules-inspector/).
Once installed, this plugin allows you to view all the existing routing rules as well
as offers a button to flush the rules.

### Controlling access to your functions
We have a custom router, which handles the URLs of the user section of our
application. Next, we need a controller to handle the requests and generate the
template for the user.

Even though we have changed the default routing, WordPress will look for an
existing template to be sent back to the user. Therefore, we need to intercept this
process and create our own templates. WordPress offers an action hook called
`template_redirect` for intercepting requests.
```php
add_action( 'template_redirect', array( $this, 'front_controller') );
public function front_controller() {
 global $wp_query;
 $control_action = isset ( $wp_query->query_vars['control_action'] ) ? $wp_query->query_vars['control_action'] : '';
  switch ( $control_action ) {
   case 'register':
   do_action( 'wpwa_register_user' );
   break;
  }
}
```
For Gmail validation, we can define another function using the following code:
```php
add_action( 'wpwa_register_user', array( $this, 'validate_gmail_registration') );
public function validate_user(){
  // Code to validate user
  // remove registration function if validation fails
  remove_action( 'wpwa_register_user', array( $this,
  'register_user' ) );
}
```
#### Designing the registration form
We will implement the custom templates inside
the plugin. First, create a folder inside the current plugin folder and name it as
templates to get things started.
We need to design a custom form for frontend registration containing the default
header and footer. The whole content area will be used for the registration and the
default sidebar will be omitted for this screen. Create a PHP file called registertemplate.
php inside the templates folder with the following code:
```php
<?php get_header(); ?>
<div id="wpwa_custom_panel">
if( isset($errors) && count( $errors ) > 0) {
 foreach( $errors as $error ){
  echo '<p class="wpwa_frm_error">'. $error .'</p>';
 }
}
?>
// HTML Code for Form
</div>
<?php get_footer(); ?>
```
Then, we have the HTML form, as shown in the following code:
```php
<form id='registration-form' method='post' action='<?php echo
get_site_url() . '/user/register'; ?>'>
<ul>
<li>
<label class='wpwa_frm_label'><?php echo __('Username','wpwa'); ?></label>
<input class='wpwa_frm_field' type='text' id='wpwa_user' name='wpwa_user' value='' />
</li>
<li>
<label class='wpwa_frm_label'><?php echo __('Email',' wpwa'); ?></label>
<input class='wpwa_frm_field' type='text' id='wpwa_email' name='wpwa_email' value='' />
</li>
<li>
<label class='wpwa_frm_label'><?php echo __('User Type','wpwa'); ?></label>
<select class='wpwa_frm_field' name='wpwa_user_type'>
<option <?php echo __('Follower','wpwa'); ?></option>
<option <?php echo __('Developer','wpwa'); ?></option>
<option <?php echo __('Member','wpwa'); ?></option>
</select>
</li>
<li>
<label class='wpwa_frm_label' for=''>&nbsp;</label>
<input type='submit' value='<?php echo __('Register','wpwa'); ?>' />
</li>
</ul>
</form>
```
Once the form is submitted, we have to create the user based on the
application requirements.
Let's begin the task of registering users by displaying the registration form
as given in the following code:
```
public function register_user() {
 if ( !is_user_logged_in() ) {
  include dirname(__FILE__) . '/templates/registertemplate.php';
  exit;
 }
}
```
Once user requests /user/register, our controller will call the `register_user`
function using the do_action call. In the initial request, we need to check whether
a user is already logged in using the `is_user_logged_in` function. If not, we can
directly include the registration template located inside the templates folder to
display the registration form. In this technique, we are including the template directly inside
the function. Therefore, we have access to the data inside this function.


