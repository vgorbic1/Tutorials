## Networking

#### ACCESSING OTHER WEB SITES
To access another website, just use ```fopen()``` function (PHP must be configured to allow for ```fopen()``` calls over network):
```PHP
fopen('http://www.example.com/', 'r');
```
The file will be opened only for reading. Use trailing slash after a directory because fopen() will not support redirects. If you put
```example.com/dir``` the server will redirect it automatically to ```example.con/dir/```

Once you are opened a file, you can treat it normally with file() or fgets() to retrieve data.
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Get Stock Quotes</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<?php // This page retrieves a stock price from Yahoo!.
if (isset($_GET['symbol']) && !empty($_GET['symbol'])) { 
    // Identify the URL:
    $url = sprintf('http://quote.yahoo.com/d/quotes.csv?s=%s&f=nl1', $_GET['symbol']);
    // Open the "file".
    $fp = fopen($url, 'r');        
    // Get the data in comma-separated-value format:
    $read = fgetcsv($fp);    
    // Close the "file":
    fclose($fp);    
    // Check the results for improper symbols:
    if (strcasecmp($read[0], $_GET['symbol']) !== 0) {
        // Print the results:
        echo '<div>The latest value for <span class="quote">' . $read[0] . '</span> (<span class="quote">' . $_GET['symbol'] . '</span>) is $<span class="quote">' . $read[1] . '</span>.</div>';      
    } else {
        echo '<div class="error">Invalid symbol!</div>';
    }
} // End of form submission IF.
// Show the form:
?><form action="get_quote.php" method="get">
    <fieldset>
        <legend>Enter a NYSE stock symbol to get the latest price:</legend>
        <p><label for="symbol">Symbol</label>: <input type="text" name="symbol" size="5" maxlength="5"></p>
        <p><input type="submit" name="submit" value="Fetch the Quote!" /></p>
    </fieldset>
</form>
</body>
</html>
```

#### SOCKETS
Using sockets is more interacting method to connect to another server. A socket is a channel through which two computers can communicate with each other. To open a socket use fsockopen() function:
```php
$fp = fsockopen($url, $sport, $error_number, $error_string, $timeout);
```
Parameters are the URL, the port, an error number variable, and error string variable, and the timeout. Only the first parameter is required.
The port is the door through which different protocols (methods of communication) go. More than 60,000 ports exist.
Timeout simply states for how many seconds the function should try to connenct.
When the socket is open use ```fwrite()``` or ```fgets()```.

Use ```parse_url()``` function to take a URL and turn it into an associative array by breaking the structure into tis parts (see manual for indexes):
```php
$url_pieces =  parse_url($url);
```
The following example script checks if the URL are still valid:
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Validate URLs</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<?php // This page validates a list of URLs. 
// This function will try to connect to a URL:
function check_url($url) { 
    // Break the URL down into its parts:
    $url_pieces = parse_url($url);    
    // Set the $path and $port:
    $path = (isset($url_pieces['path'])) ? $url_pieces['path'] :  '/'; 
    $port = (isset($url_pieces['port'])) ? $url_pieces['port'] : 80; 
    // Connect using fsockopen():
    if ($fp = fsockopen($url_pieces['host'], $port, $errno, $errstr, 30)) { 
        // Send some data:
        $send = "HEAD $path HTTP/1.1\r\n";
        $send .= "HOST: {$url_pieces['host']}\r\n";
        $send .= "CONNECTION: Close\r\n\r\n";
        fwrite($fp, $send);
        // Read in the first 128 characters of the response:
        $data = fgets($fp, 128); 
        // Close the connection:
        fclose($fp); 
        // Return the response code:
        list($response, $code) = explode(' ', $data); 
        if ($code == 200) {
            return array($code, 'good');
        } else {
            return array($code, 'bad');
        }
    } else { // No connection, return the error message:
        return array($errstr, 'bad');
    }   
} // End of check_url() function.
// Create the list of URLs:
$urls = array(
'http://www.larryullman.com/',
'http://www.larryullman.com/wp-admin/',
'http://www.yiiframework.com/tutorials/',
'http://video.google.com/videoplay?docid=-5137581991288263801&q=loose+change'
);
// Print a header:
echo '<h2>Validating URLs</h2>';
// Kill the PHP time limit (make it limitless):
set_time_limit(0);
// Validate each URL:
foreach ($urls as $url) {
    list($code, $class) = check_url($url);
    echo "<p><a href=\"$url\" target=\"_new\">$url</a> (<span class=\"$class\">$code</span>)</p>\n";
} 
?>
</body>
</html>
```

#### GEOLOCATION
IP address is stored in ```$_SERVER['REMOTE_ADDR']``` superglobal. To perform IP geolocation, you must have access to a GeoIP database, for example freegeoip.net or maxmind.com. You just need to perform GET request of a specific URL.
gethostbyname() function returns the IP address for a given domain name.
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>IP Geolocation</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<?php # ip_geo.php
// This page uses a Web service to retrieve a user's geographic location.
// This function will perform the IP Geolocation request:
function show_ip_info($ip) {     
    // Identify the URL to connect to:
    $url = 'http://freegeoip.net/csv/' . $ip;
    // Open the connection:
    $fp = fopen($url, 'r');
    // Get the data:
    $read = fgetcsv($fp);
    // Close the "file":
    fclose($fp);
    // Print whatever about the IP:
    echo "<p>IP Address: $ip<br>
    Country: $read[2]<br>
    City, State: $read[5], $read[3]<br>
    Latitude: $read[7]<br>
    Longitude: $read[8]</p>";
} // End of show_ip_info() function.
// Get the client's IP address:
echo '<h2>Our spies tell us the following information about you</h2>';
show_ip_info($_SERVER['REMOTE_ADDR']);
// Print something about a site:
$url = 'www.entropy.ch';
echo "<h2>Our spies tell us the following information about the URL $url</h2>";
show_ip_info(gethostbyname($url));
?>
</body>
</html>
```

#### cURL
This utility (client URLs) is a command-line tool for working with URLs. 
PHP can invoke cURL via the shell_exec() and other systems functions.
Provide ```curl_init()``` function the name of the URL to be accessed:
```php
$curl = curl_init('www.example.com');
```
Now ```$curl``` is a pointer (or a handle) to the transaction.

Set options to request using curl_setopt() function:
```php
curl_setopt($curl, CONSTANT, value);
```
There are lots of options that you can set! Check out PHP manual for the full list.

Use ```curl_exec()``` to execute the transaction:
```php
$result = curl_exec($curl);
```
Close the connection:
```
curl_close($curl);
```
The ```curl_getinfo()``` returns an array of information about the reansaction.
The ```curl_errno()``` and ```curl_error()``` retrieves the error number and message, should one occur.

This code will post arbitraty data to another page:
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Using cURL</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<h2>cURL Results:</h2>
<?php This page uses cURL to post data to a Web service.
// Identify the URL:
$url = 'http://localhost/service.php';
// Start the process:
$curl = curl_init($url);   
// Tell cURL to fail if an error occurs:
curl_setopt($curl, CURLOPT_FAILONERROR, 1); 
// Allow for redirects:
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, 1);
// Assign the returned data to a variable:
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
// Set the timeout:
curl_setopt($curl, CURLOPT_TIMEOUT, 5);
// Use POST:
curl_setopt($curl, CURLOPT_POST, 1);

// Set the POST data:
curl_setopt($curl, CURLOPT_POSTFIELDS, 'name=foo&pass=bar&format=csv');
// Execute the transaction:
$r = curl_exec($curl);
// Close the connection:
curl_close($curl);
// Print the results:
print_r($r);
?>
</body>
</html>
```

#### WEB SERVICES
Complex web services may use Web Service Description Language (WSDL) or Simple Object Access Protocol (SOAP).
Simple web services use Representational State Transfer (REST). PHP has to communicate the type of content being outputted if it is used as a service through a certain header. 

To send data in plain text format:
```php
header('Content-Type: text/plain');
```
To send data in CSV format:
```php
header('Content-Type: text/csv');
```
To send data in XML format:
```php
header('Content-Type: text/xml');
```
To send data in JSON format:
```php
header('Content-Type: application/json');
```
To read JSON data use ```json_encode()``` function:
```php
echo json_encode($data);
```
Creating a simple service:
```php
<?php // This script acts as a simple Web service.
      // The script only reports back the data received, along with a bit of 
      // extra information.
// Check for proper usage:
if (isset($_POST['format'])) {    
    // Switch the content type based upon the format:
    switch ($_POST['format']) {
        case 'csv':
            $type = 'text/csv';
            break;
        case 'json':
            $type = 'application/json';
            break;
        case 'xml':
            $type = 'text/xml';
            break;
        default:
            $type = 'text/plain';
            break;
    }
    // Create the response:
    $data = array();
    $data['timestamp'] = time();
    // Add back in the received data:
    foreach ($_POST as $k => $v) {
        $data[$k] = $v;
    } 
    // Format the data accordingly:
    if ($type == 'application/json') {
        $output = json_encode($data);    
    } elseif ($type == 'text/csv') {
        // Convert to a string:
        $output = '';
        foreach ($data as $v) {
            $output .= '"' . $v . '",';
        }
        // Chop off the final comma:
        $output = substr($output, 0, -1); 
    } elseif ($type == 'text/plain') {
        $output = print_r($data, 1);
    }
} else { // Incorrectly used!
    $type = 'text/plain';
    $output = 'This service has been incorrectly used.';
}
// Set the content-type header:
header("Content-Type: $type");
echo $output;
```
