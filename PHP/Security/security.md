## Security
A security-conscious mindset assumes that all data received in input is tainted and must be filtered before use and escaped
when leaving the application. Understanding and practicing these concepts is essential to ensure the security of your applications.

The main thing to remember is FIEO: Filter Input, Escape Ouput.

As a general rule of thumb, the data in all of PHP’s superglobal arrays should
be considered tainted. This is because either all or some of the data provided
in the superglobal arrays comes from an external source. Even the ```$_SERVER```
array is not fully safe, because it contains some data provided by the client.
The one exception to this rule is the ```$_SESSION``` array, which is persisted on
the server and never transmitted over the Internet.

#### Whitelist vs. Blacklist Filtering
Blacklist filtering is the less restrictive approach; it assumes the programmer knows everything that should not be allowed to pass through. Blacklists must be continually modified and expanded as new attack vectors become apparent.

Whitelist filtering is much more restrictive, but it affords the programmer the ability to accept only expected inputs. Instead of identifying data that is unacceptable, a whitelist identifies the data that is acceptable. Any inputs not on the whitelist will be rejected. Whitelists afford stronger protection against attacks than blacklists do.

#### Validation
Since all input is tainted and cannot be trusted, you must validate your input to ensure that it is what you expect. To do this, we use validation, or a whitelist approach:
```html
<form method="POST">
  Username: <input type="text" name="username"><br>
  Password: <input type="text" name="password"><br>
  Favourite colour:
  <select name="colour">
    <option>Red</option>
    <option>Blue</option>
    <option>Yellow</option>
    <option>Green</option>
  </select><br>
 <input type="submit">
</form>
```
It is possible to implement client-side validation code using JavaScript to enforce these rules, but while client-side validation is important for usability, server-side filtering is important for security.

Validation can take one of two forms; the first is comparison against known good values, and the second is confirmation of content.
```php
$clean = array();
if (ctype_alpha($_POST['username'])) {
  $clean['username'] = $_POST['username'];
}
if (ctype_alnum($_POST['password'])) {
  $clean['password'] = $_POST['password'];
}

$colours = array('Red', 'Blue', 'Yellow', 'Green');
if (in_array($_POST['colour'], $colours)) {
   $clean['colour'] = $_POST['colour'];
}
```

#### Escape Output
As you should filter all incoming data, you should escape all outbound data. Whereas filtering input protects your application from bad or harmful data, escaping output protects the client and user from potentially damaging commands. Escaping output should not be regarded as part of the filtering process, however. These two steps, while equally important, serve distinct purposes.

To escape output intended for a web browser, PHP provides ```htmlspecialchars()``` and ```htmlentities()```, the latter being the most
exhaustive and, therefore, recommended function for escaping.

For this example, assume that the value for ```$user_message``` comes from a database result set:
```php
$html = array();
$html['message'] = htmlentities($user_message, ENT_QUOTES, 'UTF-8');
echo $html['message'];
```
The database engine (or PDO, if it is emulating prepared statements) performs the hard work of actually escaping the values for use in the statement.
```php
// First, filter the input
$clean = array();
if (ctype_alpha($_POST['username'])) {
  $clean['username'] = $_POST['username'];
  // Set a named placeholder in the SQL statement
  $sql = 'SELECT * FROM users WHERE username = :username';
  // Assume the handler exists; prepare the statement
  $stmt = $dbh->prepare($sql);
  // Create our data mapping
  $data = [':username' => $clean['username']];
  // Execute and fetch results
  $stmt->execute($data);
  $results = $stmt->fetchAll();
}
```

#### Filtering
Filtering is both validation and sanitization of input. Validation confirms that the input is what we expect, while sanitization will
clean a string by either escaping or removing offending parts. Often we want to do both. PHP 5.2 added a new filter extension that allows much more control over validation, as well as the ability to do some common escaping.

**filter_input()**

The function is recommended for working explicitly with input via $_GET, $_POST, $_SERVER, $_COOKIE, $_SERVER, and $_ENV. It accepts 4 arguments:
- The type of input, which is one of the constants: INPUT_GET, INPUT_POST, INPUT_COOKIE, INPUT_SERVER, INPUT_ENV
- The variable name, which is what would be the array key of the superglobal array
- The filter to apply
- Filter options

**filter_var()**

This function will filter any variable (or constant expression), including those in the superglobal arrays (although choosing to filter individual values and expressions will make verifying security more difficult). This is very similar to ```filter_input()``` except that it only takes three arguments:
- The value to filter
- The filter to apply
- Filter options

There are two types of filters that can be applied, validation and sanitizing. All filters return the—potentially sanitized—value, or false on failure.
```php
// First, filter the input
$clean = array();
// Validate it's just a string
$username = filter_input(INPUT_POST, 'username', FILTER_VALIDATE_REGEXP, ['options' =>['regexp' => '/^[a-z]$/i']]);
// If validation failed, $username will be false
if ($username) {
  $clean['username'] = $username;
} else {
  // Validation failed, prepare the input for re-output to the user in HTML
  $clean['username'] = filter_input(INPUT_POST, 'username', FILTER_SANITIZE_SPECIAL_CHARS);
}
```
We can also specify different filters for each input value:
```php
$clean = filter_input_array(INPUT_POST, 
  [
    'email' => FILTER_VALIDATE_EMAIL,
    'blog' => FILTER_VALIDATE_URL,
    'age' => ['filter' => FILTER_VALIDATE_INT, 'options' => ['min_range' => 18]]
  ]
);
```
Be aware that FILTER_VALIDATE_URL only allows ASCII domains;
internationalized domain names (IDN) must first be converted to punycode
using idn_to_ascii(). Additionally, a valid URL does not necessarily
mean that it uses the HTTP scheme; you should validate the scheme using
parse_url().

#### More Examples
Sanities any input from a user as soon as it arrives. 

The ```htmlentities()``` function converts characters to HTML entities.
```php
$username = htmlentities($username);
 // or even better use an extra argument to sanitize all single quotes too:
$username = htmlentities($username, ENT_QUOTES);
```
To be able use all HTML tags again use ```html_entity_decode()``` function.

The ```htmlspecialchars()``` function converts special characters to HTML entities. This means that it will replace HTML characters like < and > with &lt; and &gt;. This prevents attackers from exploiting the code by injecting HTML or Javascript code (Cross-site Scripting attacks) in forms:
```html
<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>">
```
The``` $_SERVER["PHP_SELF"]``` variable can be used by hackers! If PHP_SELF is used in your page then a user can enter a slash (/) and then some Cross Site Scripting (XSS) commands to execute.

#### filter_var()
The ```filter_var()``` function filters a variable with the specified filter. 

Get filters here: http://www.w3schools.com/php/php_ref_filter.asp
```php
$email = "john.doe@example.com";
if (!filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
  echo("$email is a valid email address");
} else {
  echo("$email is not a valid email address");
}
```

#### strip_tags()
The ```strip_tags()``` function strips a string from HTML, XML, and PHP tags. HTML comments are always stripped and this cannot be changed with the allow parameter. This function is binary-safe.

Syntax:
```
strip_tags(string, allow);
```
"allow" is optional. It specifies allowable tags that will not be removed:
```php
echo strip_tags("Hello <b><i>world!</i></b>","<b>");
```
Good to use with SQL queries:
```php
$task = mysqli_real_escape_string($dbc, strip_tags($_POST['task']));
```

#### mysqli_real_escape_string()
The ```mysqli_real_escape_string()``` function escapes special characters in a string for use in an SQL statement.

Syntax:
```
mysqli_real_escape_string(connection, escapestring);
```
Example:
```php
$task = mysqli_real_escape_string($dbc, strip_tags($_POST['task']));
```
