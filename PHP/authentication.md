## Authentication

Prevent access by unauthorized users.  Combine authentication with sessions.
```PHP
<?php
  $username = '';
  $password = '';
  session_start() != FALSE
    or die('Could not start session');
  if (isset($_SESSION['username'])) $username = $_SESSION['username'];
  if (isset($_SESSION['password'])) $password = $_SESSION['password'];
  echo <<<_EOT
<!DOCTYPE html>
<html>
  <head>
    <title>Using Sessions</title>
  </head>
  <body>
    <h2>You are currently logged in as '$username'</h2>
    (And your password is: '$password')
  </body>
</html>
_EOT;
?>
```
To close session use this code before any part of HTML on the page:
```PHP
function CloseSession() {
  $SESSION = array();
  if (session_id() != '' || isset($COOKIE[session_name()]))
    setcookie(session_name(), '', time() – 3600, '/');
  session_destroy();
}
```
To make sure the user has cookies enabled:
```PHP
ini_set('session.use_only_cookies', 1);
```

