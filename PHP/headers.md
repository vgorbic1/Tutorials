## Headers

Headers are a little text messages with specific instructions on what is being requested or delivered. 
Use a ```header()``` function to create a custom header. Make sure there is no character of space before the header request, because the browser will reject it. The header should be very first thing sent to the browser in a PHP file.

#### Location Header
Location header redirects a page to another specific page:
```php
<?php header(‘Location: http://specificpage.com’); ?>
```

#### Refresh Header
Refresh header refreshes a page after a period of time has elapsed:
```php
<?php header(‘Refresh: 5, url= http://specificpage.com’); ?>
```

#### Content Type Header
This header controls the type of the content being delivered by the server. You can force a page to be a plain text:
```php
<?php header(‘Content-Type: text/plain’); ?>
```

Basic authentication code
```php
<?php
  // User name and password authentication
  $username = 'user';
  $password = 'pass';
  // Get the username and password from the authentication window
  if (!isset($_SERVER['PHP_AUTH_USER']) || !isset($_SERVER['PHP_AUTH_PW']) || 
	 ($_SERVER['PHP_AUTH_USER'] != $username) || ($_SERVER['PHP_AUTH_PW'] != $password)) {
		// In case the user name / password are incorrect, send the following authentication headers:
header('HTTP/1.1 401 Unauthorized');
// Define security zone with realm
header('WWW-Authenticate: Basic realm="Guitar Wars" ');
exit('<h2>Guitar Wars</h2>Sorry, you must enter a valid user name and password to access this page.');
  }
        // In case the user name and password is correct, display the rest of the page:
?>
<!DOCTYPE html>
…
```
