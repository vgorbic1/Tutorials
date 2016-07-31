## Sessions
A session ensures continuity by storing a random identifier on the web server and on the visitor's computer as a cookie. The web server uses the cookie to recognize that it is communicating with the same computer. When a session is initiated, the server stores information in session variables that can be accessed by other pages as long as the session remains active (normally until the browser is closed). Because the identifier is unique to each visitor, the information stored in session variables cannot be seen by anyone else.

The only information stored on the user's computer is the cookie that contains the identifier, which is meaningless by itself. The session variables and their values are stored on the web server.

If several people share the same computer, they all have access to each other's sessions unless they always close the browser before handing over to the next person. It is important to provide a logout mechanism to delete both the cookie and the session variables, keeping your site secure. You can also create a timeout mechanism, which automatically pervents anyone regaining access after a certain period of inactivity.

Although sessions are generally secure enough for password protecting parts of a website, you should never use session variables to store sensitive information, such as passwords or credit catd details. Password should be stored (preferably encrypted) in a separate loacation, and not as a session variable.

Sessions are supported by default and don't need any special configuration. However, since they rely on a cookie, sessions won't work if cookies are disabled in the user's browser.

#### Creating PHP sessions
To create a session just put the following in every PHP page that you want to use in a session:
```php
session_start();
```
It should be placed immediatelly after openning PHP tag.

#### Creating and destroying session variables
If you need to store a name submitted in a form:
```php
$_SESSION['name'] = $_POST['name'];
```
No the session variable ```$_SESSION['name']``` can be used in any page that begins with ```session_start()```.

Because session variables are stored on the server, you should get rid of them as soon as they are no longer required by your srcript:
```php
unset($_SESSION['name']);
```
To unset all session variables at once:
```php
$_SESSION = array();
```
Do not use ```unset($_SESSION)``` which prevents any further sessions from being stored.

#### Destroying a session
To invalidate session cookie:
```php
if (isset($_COOKIE[session_name()]) {
  setcookie(session_name(), '', time()-86400, '/');
}
session_destroy();
```
The function ```session_name()``` gets the name of the session dynamically. '/' applies cookie to the whole domain.

#### Using sessions to restrict access
Create a simpe script (three files) that display session usage. Create a simple form```session-test.html```:
```html
<!DOCTYPE html>
<html>
<body>
<form id="form1" name="form1" action="session.php" method="post">
  <p>
    <label for="name">Name:</label>
    <input type="text" name="name" id="name" />
  </p>
  <p>
    <input type="submit" name="submit" value="Submit">
  </p>
</form>
</body>
</html>
```
Create a ```session.php``` file:
```php
<?php
session_start();
if ($_POST && !empty($_POST['name'])) {
	$_SESSION['name'] = $_POST['name'];
}
?>
<!DOCTYPE html>
<html>
<body>
<?php 
if (isset($_SESSION['name'])) {
	echo 'Hi, ' . $_SESSION['name'] . '. <a href="session-next.php">Next</a>';	
} else {
	echo 'Who are you? <a href="session-test.html">Login</a>';
}
?>
</body>
</html>
```
Create ```session-next.php``` file:
```php
<?php 
session_start();
ob_start(); // start output buffer. We need it for setcookie() functioning in the body of the document.
?>
<!DOCTYPE html>
<html>
<body>
<?php
if (isset($_SESSION['name'])) {
	echo 'Hi, ' . $_SESSION['name'] . '. See, I remember you!';
	unset($_SESSION['name']);
	if (isset($_COOKIE[session_name()])) {
		setcookie(session_name(), '', time()-86400, '/');
	}
	ob_end_flush(); // flush output buffer. We are done with setcookie().
	session_destroy();
	echo '<a href="session.php">Back</a>'; 
} else {
	echo 'Sorry, I don\'t know you.<br />';
	echo '<a href="session-test.html">Login</a>';
}
?>
</body>
</html>
```
