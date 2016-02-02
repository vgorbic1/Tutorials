## Superglobals
Superglobals are predefined variables and can be accessed anywhere in the script. 

- `$GLOBALS[]` An associative array containing references to all variables that are currently defined in the global scope of the script. It is an easy way to access global variable without specifying it as global to a function by using the global keyword.

- `$_SERVER[]` An associative array containing information such as headers, paths and script locations. The entities in this array are created by the server and there is no guarantee that every web server will provide any or all of these.

- `$_GET[]` An associative array of variables passed to the current script via the HTTP GET method.

- `$_POST[]` An associative array of variables passed to the current script via the HTTP POST method.

- `$_FILE[]` An associative array of items uploaded to the current script via the HTTP POST method.

- `$_COOKIE[]` An associative array of variables passed to the current script via HTTP Cookies.

- `$_SESSION[]` An associative array containing session variables available to the current script.

- `$_REQUEST[]` An associative array that by default contains the contents of $_GET[], $_POST[], and $_COOKIE[].

- `$_ENV[]` An associative array of variables passed to the current script via the environment method.

You should always sanitize before using global variables, since they can by loaded with malicious code!
```PHP
$message = htmlentities($_GET['message']);
```

#### SERVER
- `$_SERVER['PHP_SELF']` Stores the name of the current script. Used to replace the form action URL to make a self-referenced form (sticky form):
```PHP
<form action=”<?php echo $_SERVER[‘PHP_SELF’]; ?>” method=”post”>
```
- `$_SERVER['PHP_AUTH_USER']` Stores the user name entered into the authentication window.
- `$_SERVER['PHP_AUTH_PW']` Stores the password entered into the authentication window.
- `$_SERVER['HTTP_REFERER']` gets the url of the page the user came from.

#### FILES
- `$_FILES` Stores information passed to the server by the form about the downloaded file. Make sure that the form has the following tag:
<form enctype="multipart/form-data" >
```
<input type="file" name="screenshot" />
```
- `$_FILES['screenshot']['name']` to get the name of uploaded file. This should be always stripped out before being used! Like this: 
```PHP
$name = strtolower(preg_replace('/[^\w.-]/', '', $_FILES['file']['name']));
```
- `$_FILES['screenshot']['type']` to get the MIME type of the file. The MIME could be:

Applications: application/pdf, application/zip

Audio: audio/mpeg, audio/x-wav

Images: image/gif, image/jpeg, image/png, image/tiff

Text: text/html, text/plain, text/xml

Video: video/mpeg, video/mp4, video/quicktime

- `$_FILES['screenshot']['size']` to get the size in bytes.
- `$_FILES['screenshot']['tmp_name']` to get a temporary storage location.
- `$_FILES['screenshot']['error']` to get an error code. 0 indicates success.
- `$_FILES[]` array is cleared when PHP exits, so if you do not copy an uploaded file to a permanent location, it will be lost on exit.

#### COOKIE
- `$_COOKIE` Used to retrieve the value of cookie.
```PHP
echo(‘ You are logged as ‘ . $_COOKIE[‘cookie_name’]);
```

#### SESSION
- `$_SESSION` Used to store and retrieve session variables. No need for special PHP functions to set these variables.
```PHP
$_SESSION['username'] = 'my_usernime';
```
To delete all session variables just set the superglobal to an empty array:
```PHP
$_SESSION = array();
```

#### SID
- `SID` Holds session ID.
```PHP
<?php echo SID; ?>
```
