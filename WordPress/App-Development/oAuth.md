## OpentAuth on a Portfolio Application Example
The portfolio application will contain the OpenAuth login
using Twitter, Facebook, and LinkedIn. So, we need three links or buttons just
under our login screen.

We have two ways of assigning these links into the login screen:
1. Directly embed the HTML code under the default login button.
2. Define an action hook and implement the hook within a plugin.

Even though both techniques does the same job, we have more advantage in
choosing the action hooks technique as it allows us to add or remove any number
of login-related components without affecting existing functionality.
```php
<?php do_action('wpwa_social_login'); ?>
```
This allows the possibility of adding dynamic content to the login screen using plugins.
Next, we have to generate the necessary login links to populate the wpwa_social_
login area. Create a new class called WPWA_Social in a file called class-wpwasocial.
php for including the functions related to social login links. The first task is
to create the login links for different social networks and add them to the login form.
Let's look at the initial version of WPWA_Social class:
```php
<?php
class WPWA_Social{
 public function __construct(){
  /* Add the social login buttons to the registration and login forms based on the settings */
  add_action('wpwa_social_login', array($this,'wpwa_social_login_buttons'));
 }
 public function wpwa_social_login_buttons($html){
  $allowed_networks = array('Twitter','Linkedin','Facebook');
  if (get_option('users_can_register') == '1') {
   $html = '<div align="center" style="margin:10px">';
   foreach ($allowed_networks as $key => $network) {
    $link = '?wpwa_social_login='.$network.'&wpwa_social_action=login';
    $html .= '<a class="wpwa-social-link" href="' . $link . '" >
    Login with '. $network .'</a>';
   }
   $html .= '</div>';
  }
  echo $html;
 }
}

$social_obj = new WPWA_Social();
```
The `href` attribute contains the action to be executed and the name of the social network.

### Configuring login strategies
We need to implement the login strategy for each social network. So, we need a base
class for handling common functionality for all the social networks. Let's create a
new class called` WPWA_Social_Connect` inside a file called class-wpwa-socialconnect.
php. This file needs to be created in the root of our plugins folder. As
usual, we need to include this file inside class-wpwa-portfolio-manager.php
using a `require_once` statement.
```php
<?php
class WPWA_Social_Connect{
  public function callback_url(){
    $url = 'http://' . $_SERVER["HTTP_HOST"] . $_SERVER["PHP_SELF"];
    if(strpos($url, '?')===false){
      $url .= '?';
    }else{
      $url .= '&';
    }
    return $url;
  }
  public function redirect($redirect){
    wp_redirect($redirect);exit;
  }
  public function register_user($result){}
}
```
These are the most common functions for all the social networks at this stage.
However, we might need additional functions as we cater to advanced requirements
of social login. First, we have a function called callback_url for defining the the
return page after completing the authentication with the social network. We use the
current page URL as the callback URL. Then, we have a generic function for making
the redirections using the wp_redirect function. Finally, we have the register_user
function. This function will be used to either register a new user or login existing
user, after successful authentication with social network. Now, we have the base
functionality to implement the social login.

In this example, we will implement a social login with LinkedIn. We omit other
networks, as the process is similar. So first, we need to find an OAuth library and
LinkedIn API library. The OAuth library provided by https://code.google.
com/p/oauth/ is the popular choice among developers. You can select the PHP
version and grab the OAuth.php class. Since it's a library, we will create a new
folder called lib inside our main plugin. We can place the OAuth.php class inside
the lib folder and will require it in our main plugin file as usual.

Then, we can grab a library for LinkedIn API functions at https://code.google.
com/p/simple-linkedinphp/. This is the most popular and simplest choice. You
can download the library and copy the linkedin_3.2.0.class.php file into lib\
LinkedIn folder. As usual, we need to require this file from our main plugin file.

We created a class called WPWA_Social for all the common functionality for social login. So, we
need to create a class for each social network and extend the WPWA_Social class for
the common functionality. Let's create a new class called WPWA_LinkedIn_Connect
in a file called class-wpwa-linkedin-connect.php. This file needs to be included
after the Oauth.php and linkedin_3.2.0.class.php files. First, we need to identify
the functionality of this class as follows:
- This class should redirect the user to the respective social network to
authorize the account with our application
- Once account is authorized and redirected to our site, we need to verify
the account details and log in the user
- We need to handle any errors generated from the social network

Let's start with redirecting to LinkedIn and authorizing the application. The
following code shows the initial implementation of the WPWA_LinkedIn_Connect
class with the login function:
```php
<?php
class WPWA_LinkedIn_Connect extends WPWA_Social_Connect{
 public function login(){
  $callback_url = wpwa_add_query_string($this->callback_url(), 'wpwa_social_login=Linkedin&wpwa_social_action=verify');
  $wpwa_social_action = isset($_GET['wpwa_social_action']) ? $_GET['wpwa_social_action'] : '';
  $response = new stdClass();
  /* Configuring settings for LinkedIn application */
  $app_config = array(
   'appKey' => 'app key',
   'appSecret' => 'app secret',
   'callbackUrl' => $callback_url
  );
  @session_start();
  $linkedin_api = new LinkedIn($app_config);
  if ($wpwa_social_action == 'login'){
   /* Retrive access token from LinkedIn */
   $response_linkedin = $linkedin_api->retrieveTokenRequest(array('scope'=>'r_emailaddress'));
   if($response_linkedin['success'] === TRUE) {
     /* Redirect the user to LinkedIn for login and authorizing the application */
     $_SESSION['oauth']['linkedin']['request'] = $response_linkedin['linkedin'];
     $this->redirect(LINKEDIN::_URL_AUTH . $response_linkedin['linkedin']['oauth_token']);
   }else{
     // Handle Error
   }
  }
  return $response;
 }
}
```
We start the implementation by extending the WPWA_Social_Connect class. Consider
the first three lines of the login function. We add the wpwa_social_login and
wpwa_social_action parameter to the callback URL generated from the parent class.
Here, we have used a custom function called wpwa_add_query_string, to add the
query variables to the callback URL. Implementation of the wpwa_add_query_string
function can be found inside the functions.php file of the main plugin. Then, we
assign the action to the $wpwa_social_action variable and create a stdClass object
to handle the response.

Afterwards, we have to define the LinkedIn app key and secret in the $app_config
array, along with the callback URL.

Now, we can start the process of authenticating user account with our application.
First, we start a new session using session_start to hold the data retrieved
from LinkedIn. Then, we initialize the third-party LinkedIn class by passing the
$app_config array. We have to check for the proper action using $wpwa_social_
action as we have multiple actions in this process. If the action is login, we call
the retrieveTokenRequest function of LinkedIn API class with a scope called
r_emailaddress. You can learn more about scope in LinkedIn API at https://
developer.linkedin.com/documents/authentication.

Then, we save the information to session and redirect the user to LinkedIn on a
successful response from the retrieveTokenRequest function execution. If this
function generates any errors, we need to handle it using a custom function. We will
be omitting the error handling part considering the scope of this chapter. You will find
complete implementation on the book website. After redirecting to LinkedIn, the user
can authenticate the application with their LinkedIn account. Once the authentication
is completed, the request will be redirected to our application using the callback URL.
So, we need to start the implementation to verify account details and log in the user,
as we discussed in point 2 on the functionality of the WPWA_LinkedIn_Connect class.

## Verifying LinkedIn account and generating response
We created an if statement in the previous code to check for the availability of the
login action. Now, we need to extend it with the else if statement to check for the
response from LinkedIn. The following code contains the implementation of account
verification process:
```php
elseif(isset($_GET['oauth_verifier'])){
$response_linkedin = $linkedin_api-
>retrieveTokenAccess($_SESSION['oauth']['linkedin']['request']['oa
uth_token'],
$_SESSION['oauth']['linkedin']['request']['oauth_token_secret'],
$_GET['oauth_verifier']);
if($response_linkedin['success'] === TRUE){
$linkedin_api-
>setTokenAccess($response_linkedin['linkedin']);
$linkedin_api-
>setResponseFormat(LINKEDIN::_RESPONSE_JSON);
$user_result = $linkedin_api->profile('~:(emailaddress,
id,first-name,last-name,picture-url)');
if($user_result['success'] === TRUE) {
/* setting the user data object from the response */
$data = json_decode($user_result['linkedin']);
$response->status = TRUE;
$response->wpwa_network_type = 'linkedin';
$response->first_name = $data->firstName;
$response->last_name = $data->lastName;
$response->email = $data->emailAddress;
$response->username = $data->emailAddress;
$response->error_message = '';
}else{
/* Handling LinkedIn specific errors */
}
}else{
/* Handling LinkedIn specific errors */
}
}
```
The LinkedIn API redirects the request to our application with a URL parameter
called oauth_verifier, and hence, we check the existence of the parameter before
proceeding. Once its set, we call the retrieveTokenAccess function of API class
with session parameters and the value of oauth_verifier. This function verifies the
request and requests the users access token from the Linkedin API. Once successful,
the response is returned and we call the setTokenAccess and setResponseFormat
functions of API class. Having completed the verification process, we can now
request the user details using the access tokens generated earlier. So, we execute
the profile function of the API class with necessary information such as emailaddress,
id, first-name, last-name, picture-url, and so on. Once the profile
information request is successful, we assign the necessary profile data to our
response object.

Now, we can move back to the configuration array in the login function and
include the LinkedIn configuration details, as shown in the following code:
```php
$app_config = array(
'appKey' => 'h8274rwoerp1',
'appSecret' => 'W7xE1KINoDajgl0a',
'callbackUrl' => $callback_url
);
```
We have completed the implementation of the WPWA_LinkedIn_Connect class.
Now, we need to initialize this process and log in the users into our application.

### Initializing the library
We have implemented all the functionality for authenticating users from LinkedIn,
using WPWA_LinkedIn_Connect and WPWA_Social classes. However, nothing will
work yet as we haven't initialized the social login library class. So, we have
to implement the initialization code inside the WPWA_Social class. Let's start the
process by including a wp_loaded action to execute the initialization. The following
code displays the modified constructor of the WPWA_Social class:
```php
public function __construct(){
add_action('wp_loaded', array($this,
'wpwa_social_login_initialize'));
add_action('wpwa_social_login', array($this,
'wpwa_social_login_buttons'));
}
```
Next, we need to implement the wpwa_social_login_initialize function,
as shown in the following code:
```php
public function wpwa_social_login_initialize(){
$wpwa_social_login_obj = false;
$wpwa_social_login = isset($_GET['wpwa_social_login']) ?
$_GET['wpwa_social_login'] : '';
$wpwa_social_action = isset($_GET['wpwa_social_action']) ?
$_GET['wpwa_social_action'] : '';
if('' != $wpwa_social_login ){
switch ($wpwa_social_login) {
case 'Linkedin':
$wpwa_social_login_obj = new
WPWA_LinkedIn_Connect();
break;
default:
break;
}
if($wpwa_social_login_obj){
$login_response = $wpwa_social_login_obj->login();
}
}
}
First, we retrieve the wpwa_social_login and wpwa_social_action variables from
the $_GET array. We will check the existence of the wpwa_social_login variable
before proceeding further. Then, we switch the wpwa_social_login variable to
identify the social network. Here, we have only included LinkedIn as we are only
implementing the LinkedIn version in this chapter. You can add the remaining
networks once you complete the implementation.

So, we initialize the WPWA_LinkedIn_Connect class using the $wpwa_social_login_
obj object. Finally, we check the availability of valid object in the $wpwa_social_
login_obj variable. Then, we call the login function to start the authentication process
for social login. When the user is redirected to LinkedIn, a screen will
appear asking the user to authenticate the application by logging in.
LinkedIn will redirect the user to our application once a user grants the permissions
for the application. The callback URL configured in the $app_config file will be used
as the redirection path. The next step in this process is to handle the response and
authenticate the user into our application.

### Authenticating users to our application
Once a user is successfully authenticated inside LinkedIn, the request will be
redirected to our application with the profile details of the user. However, each of these
services will provide different types of data, and hence, it's difficult to match them into
a common format. As developers, we should be relying on the most basic and common
data across all services for OpenAuth login and registrations. Let's understand the
process of authentication before moving into the response handling part:
- User clicks on the LinkedIn link
- User is redirected to LinkedIn for granting permissions to our application
- User is redirected back to our application on successful authentication with
profile details
- Application checks whether user already exists using the username
- Existing users will be automatically logged into the WordPress application
- Non-existing users will be saved in the application as a new user, using the
details retrieved from LinkedIn and redirected to profile for completing
remaining details

Now, let's see how we can handle the response object generated from the
WPWA_LinkedIn_Connect class, to authenticate users into our application. First,
we have to update the wpwa_social_login_initialize function as follows to
include the call to the register_user function:
```php
public function wpwa_social_login_initialize(){
$wpwa_social_login_obj = false;
$wpwa_social_login = isset($_GET['wpwa_social_login']) ?
$_GET['wpwa_social_login'] : '';
$wpwa_social_action = isset($_GET['wpwa_social_action']) ?
$_GET['wpwa_social_action'] : '';
if('' != $wpwa_social_login ){
switch ($wpwa_social_login) {
case 'Linkedin':
$wpwa_social_login_obj = new WPWA_LinkedIn_Connect();
break;
default:
break;
}
if($wpwa_social_login_obj){
$login_response = $wpwa_social_login_obj->login();
$wpwa_social_login_obj->register_user($login_response);
}
}
}
```
Now, we can take a look at the implementation of the register_user function
inside WPWA_Social_Connect. Let's start with the first part of this function using
the following code:
```php
public function register_user($result){
if($result->status){
if($result->wpwa_network_type != 'twitter'){
$user = get_user_by('email',$result->email);
}else{
$user = get_user_by('login',$result->username);
}
// Remaining Code
}else{
// Handle Errors
}
}
```
We start the process by checking the status of the $result object. This is the
response object generated after authenticating the account with LinkedIn. If a
successful response is received, we check the network type for login. We assigned
the network type inside the login function of the WPWA_LinkedIn_Connect class.
We have to do the error handling part for unsuccessful responses. There are some
key points we need to know about the username before moving forward.

Both the LinkedIn and Facebook API provide the e-mail address of the
user, and hence, we use it to verify the users. However, the Twitter
API doesn't provide an e-mail address, and hence, we have to use the
Twitter username for verifying the user account.

So, we get the user by login (username) for Twitter and user by email for other
social network. If the user is already registered with the given login or email, we
will get a valid $user object. Otherwise, it will return false. Now, we can move
into the next section of the register_user function:

```php
public function register_user($result){
if($result->status){
// Retrieving the user from the database
if(!$user){
// Create a new user for the application
}else{
// Automatically authenticating existing users
}
wp_redirect(admin_url('profile.php'));
}else{
// Handle Errors
}
```
A valid object for $user means that the existing user is trying to log in through the
LinkedIn connect. So, we authenticate and automatically log on the user and redirect
to the profile page of WordPress backend. If valid user is not found, the user is trying
to login through LinkedIn connect for the first time, and hence, we have to create a
new account for the user. Let's start by looking at the user creation process inside
the if statement:
```php
if($result->wpwa_network_type != 'twitter'){
$username = strtolower($result->first_name.$result->last_name);
if(username_exists($username)){
$username = $username.rand(10,99);
}
}else{
$username = $result->username;
}
$sanitized_user_login = sanitize_user($username);
$user_pass = wp_generate_password(12, false);
/* Create the new user */
$user_id = wp_create_user($sanitized_user_login, $user_pass,
$result->email);
if (!is_wp_error($user_id)) {
update_user_meta($user_id, 'user_email', $result->email);
update_user_meta($user_id, 'wpwa_network_type', $result-
>wpwa_network_type);
wp_update_user( array ('ID' => $user_id, 'display_name' =>
$result->first_name.' '.$result->last_name) ) ;
wp_set_auth_cookie($user_id, false, is_ssl());
}
```
We already mentioned that the Twitter API provides the username for the user,
and hence, we can use the same username for our application. The Facebook and
LinkedIn APIs don't provide a username. So, we have to build a dynamic custom
username using a combination of first and last names. However, the first and last
name combination may not be a unique username. In such cases, we add a dynamic
random number to the end of the username to make it unique. Then, we use the
sanitize_user function for stripping out unsafe characters and generate the
password using the wp_generate_password function.

Finally, we create a new user by passing username, password, and e-mail to the
wp_create_user function. If the user creation is successful, we update the user with
first and last names in the wp_users table. We also add the user e-mail and network
type to the wp_usermeta table. Next, we will use the wp_set_auth_cookie function
to create the authentication cookies for WordPress and log on the user automatically.
Once registered, the user will be authenticated by setting the WordPress authenticate
cookie and redirected to the profile page to fill out their details. At this stage, the user
will have a default password. Therefore, it's mandatory to update the user profile
with a new password to complete the registration.

Now, we can have a look at the else part of the code for existing users. It's pretty
simple as we only have to automatically log on the existing users. So, we use the
following line to create authenticate cookies and log on the user:
```php
wp_set_auth_cookie($user->ID, false, is_ssl());
```
We have completed the user registration and login process using social networks.
The intention of this implementation was to learn how to integrate third-party open
source libraries into WordPress web applications. So, we choose the OpenAuth
library and LinkedIn API class for integrating third-party services for OpenAuth
login. Now, we have completed the library integration and OpenAuth login. Make
sure that you test the user registration and login using different services.
