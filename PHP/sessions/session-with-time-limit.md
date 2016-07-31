## Setting a time limit on sessions
When the session first starts, typically when the user logs in, store the current time in a session variable. Then compare it with the lates time whenever the user does anything that treiggers a page to load. If the difference is greater than a predetermined limit,  destroy the session and its variables. Otherwise, update the variables to the latest time.

You need to store the current time after the user's credentials have been authenticated, but before the script redirects the user to the restricted part of the site.
```php
// if the session variable has been set, redirect
if (isset($_SESSION['authenticated'])) {
  // get the time the session started
  $_SESSION['start'] = time();
  header('Location: http://site.com/menu.php');
  exit;
}
```
Show a message if the session is expired:
```php
if (isset($_GET['expired'])) { ?>
  <p>Your session has expired. Please log in again.</p>
<?php } ?>
```
Create checking mechanism
```php
<?php
session_start();
ob_start();
// set a time limit in seconds
$timelimit = 15 * 60; // 15 minutes
// get the current time
$now = time();
// where to redirect if rejected
$redirect = 'http:// ';
// if session variable is not set, redirect to login page
if (!isset($_SESSION['authenticated'])) {
  header("Location: $redirect");
  exit;
// if timelimit has expired, destroy session and redirect
elseif ($now > $_SESSION['start'] + $timelimit) {
  // empty the $_SESSION array
  $_SESSION = array();
  // invalidate the session cookie
  if (isset($_COOKIE[session_name()])) {
    setcookie(session_name(), '', time()-86400, '/');
  }
  // end session and redirect with query string
  session_destroy();
  header("Location: {$redirect}?expired=yes");
  exit;
  }
// if it's got this far, it's OK to update strart time
else {
  $_SESSION['start'] = time();
}
?>
```
