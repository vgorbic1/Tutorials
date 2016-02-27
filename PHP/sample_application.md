## Sample Application
First create a configuration file

#### Configuration File
Configuration file serves for:
*	Defining constants
*	Establishing site-wide settings
*	Creating user functions
*	Managing errors
```php
<?php # Script 2.1 - config.inc.php
/* 
 *  File name: config.inc.php
 *  Created by: 
 *  Contact: 
 *  Last modified: 
 *  
 *  Configuration file does the following things:
 *  - Has site settings in one location.
 *  - Stores URLs and URIs as constants.
 *  - Sets how errors will be handled.
 */

# ***** SETTINGS ***** #
// Errors are emailed here:
$contact_email = 'address@example.com'; 

// Determine whether we're working on a local server
// or on the real server:
$host = substr($_SERVER['HTTP_HOST'], 0, 5);
if (in_array($host, array('local', '127.0', '192.1'))) {
    $local = TRUE;
} else {
    $local = FALSE;
}

// Determine location of files and the URL of the site:
// Allow for development on different servers.
if ($local) {
    // Always debug when running locally:
    $debug = TRUE;
    // Define the constants:
    define('BASE_URI', '/path/to/html/folder/');
    define('BASE_URL', 'http://localhost/directory/');
    define('DB', '/path/to/mysql.inc.php');
} else {
    define('BASE_URI', '/path/to/live/html/folder/');
    define('BASE_URL', 'http://www.example.com/');
    define('DB', '/path/to/live/mysql.inc.php');
}
    
/* 
 *  Most important setting!
 *  The $debug variable is used to set error management.
 *  To debug a specific page, add this to the index.php page:
if ($p == 'thismodule') $debug = TRUE;
require('./includes/config.inc.php');
 *  To debug the entire site, do
$debug = TRUE;
 *  before this next conditional.
 */

// Assume debugging is off. 
if (!isset($debug)) {
    $debug = FALSE;
}

# ***** SETTINGS ***** #

# ***** ERROR MANAGEMENT ***** #

// Create the error handler:
function my_error_handler($e_number, $e_message, $e_file, $e_line, $e_vars) {
    global $debug, $contact_email;
    
    // Build the error message:
    $message = "An error occurred in script '$e_file' on line $e_line: $e_message";
    
    // Append $e_vars to the $message:
    $message .= print_r($e_vars, 1);
    
    if ($debug) { // Show the error.
        echo '<div class="error">' . $message . '</div>';
        debug_print_backtrace();
    } else { 
        // Log the error:
        error_log ($message, 1, $contact_email); // Send email.
        // Only print an error message if the error isn't a notice or strict.
        if ( ($e_number != E_NOTICE) && ($e_number < 2048)) {
            echo '<div class="error">A system error occurred. We apologize for the inconvenience.</div>';
        }
    } // End of $debug IF.
} // End of my_error_handler() definition.

// Use my error handler:
set_error_handler('my_error_handler');

# ***** ERROR MANAGEMENT ***** #
```

#### Index File
The index page is the main script in the modularized application. It is also called a bootstrap file. 
The index file assembles all the proper pieces to make the complete web page. 
* Include a configuration file
* Include a database connectivity file
* Incorporate an HTML template
* Determine and include the proper content module
Bootsrtrap files do not contain any HTML at all. All the requisite HTML will be placed in included files. Name the bootstrap file index.php
```php
<?php # Script 2.4 - index.php
/* 
 *  This is the main page. This page includes the configuration file, 
 *  the templates, and any content-specific modules.
 */

// Require the configuration file before any PHP code:
require('./includes/config.inc.php');

// Validate what page to show:
if (isset($_GET['p'])) {
    $p = $_GET['p'];
} elseif (isset($_POST['p'])) { // Forms
    $p = $_POST['p'];
} else {
    $p = NULL;
}

// Determine what page to display:
switch ($p) {

    case 'about':
        $page = 'about.inc.php';
        $page_title = 'About This Site';
        break;
    
    case 'contact':
        $page = 'contact.inc.php';
        $page_title = 'Contact Us';
        break;
    
    case 'search':
        $page = 'search.inc.php';
        $page_title = 'Search Results';
        break;
    
    // Default is to include the main page.
    default:
        $page = 'main.inc.php';
        $page_title = 'Site Home Page';
        break;
        
} // End of main switch.

// Make sure the module file exists:
if (!file_exists('./modules/' . $page)) {
    $page = 'main.inc.php';
    $page_title = 'Site Home Page';
}

// Include the header file:
include('./includes/header.html');

// Include the content-specific module:
// $page is determined from the above switch.
include('./modules/' . $page);

// Include the footer file to complete the template:
include('./includes/footer.html');

?>
```

#### Modules
The modules are where content is sitting. The modules should not be loadable directly. Every module should have some code that redirects the user to the proper page, if accessed directly.
```php
<?php # Script 2.5 - main.inc.php
/* 
 *  This is the main content module.
 *  This page is included by index.php.
 */
// Redirect if this page was accessed directly:
if (!defined('BASE_URL')) {

    // Need the BASE_URL, defined in the config file:
    require('../includes/config.inc.php');
    
    // Redirect to the index page:
    $url = BASE_URL . 'index.php';
    header ("Location: $url");
    exit;
    
} // End of defined() IF.
?>
<h1>Welcome to the colour_blue template</h1>
<p>This standards compliant, simple, fixed width website template is released as an 'open source' design (under a <a href="http://creativecommons.org/licenses/by/3.0">Creative Commons Attribution 3.0 Licence</a>), which means that you are free
to download and use it for anything you want (including modifying and amending it). All I ask is that you leave the 'design from HTML5webtemplates.co.uk' link in the footer of the template, but other than that...</p>
<p>This template is written entirely in <strong>HTML5</strong> and <strong>CSS</strong>, and can be validated using the links in the footer.</p>
<p>You can view more free HTML5 web templates <a href="http://www.html5webtemplates.co.uk">here</a>.</p>
<p>This template is a fully functional 5 page website, with an <a href="examples.html">examples</a> page that gives examples of all the styles available with this design.</p>
<h2>Browser Compatibility</h2>
<p>This template has been tested in the following browsers:</p>
<ul>
  <li>Internet Explorer 8</li>
  <li>Internet Explorer 7</li>
  <li>FireFox 3.5</li>
  <li>Google Chrome 6</li>
  <li>Safari 4</li>
</ul>
```

#### Improve SEO
Use Apache mod_rewrite to prettify the site's URL. There are two ways to do it:
* Change Apache's httpd.conf file. (preferable, since Apache reads it one time when server starts)
* Create .htaccess file and place it in web directory. (Apache reads it with every request)
To restrict using .htaccess, change httpd.conf file to:
```
<Directory /> 
  AllowOverride None
</Directory>
```
Here,  in <Directory /> the "/" symbol means the root of computer. Write a path to directory that you want to restrict from overriding with .htaccess. Otherwise use flags to specify what to override:
```
<Directory /path/to/site>
  AllowOverride AutoConfig FileInfo
</Directory>
```
To alow overriding by .htaccess use:
```
<Directory "C:/xamp/htdocs/ch02">
  AllowOverride All
</Direcory>
```
Restart Apache!

Do deny all access to a directory's contents, place the following to .htaccess:

Disable directory browsing:
```
Options All -Indexes
Prevent folder listing:
IndexIgnore *
```
Prevent access to any file:
```
<FilesMatch "^.*$">
  Order Allow,Deny
  Deny from all
</FilesMatch>
```
Enabling URL Rewriting

.htaccess file must first check for the module and turn on the rewrite engine:
```
<IfModule mod_rewrite.c>
  RewriteEngine on
  RewriteBase /ch1/
  ## Add rules here ##
</IfModule>
```
RewriteBase tells where to start rewriting.

Rules may be like this:
```
  RewriteRule somepage.php otherpage.php
```
Everytime a user goes to somepage.php the contetns displayed will be from otherpage.php, but the url will say somepage.php
```
  RewriteRule ^category/([0-9]+)/?$
  category.php?id=$1
```
Here "^" means starting after rewrite base value, "+" means any number of previous character(s) or grouping, "?" means optional previous character(s) or grouping, and "$" means the end of the match. "$1" means a backreference to the first parenthetical grouping in the match, e.g. something between "(" and ")"

