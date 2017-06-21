## HTTP API
### Make HTTP Requests in PHP
#### Using HTTP Extension
```php
$r = new HttpRequest( 'http://wordpress.org/', HttpRequest::METH_GET );
$r->send();
echo $r->getResponseBody();
```
#### Using fopen() Stream
```php
if ($stream = fopen( 'http://wordpress.org/', 'r')) {
  echo stream_get_contents($stream);
  fclose($stream);
}
```
#### Using a Standard fopen()
```php
$handle = fopen( 'http://wordpress.org/', 'rb');
$contents = '';
while(!feof($handle)) {
 $contents .= fread( $handle, 8192 );
}
fclose( $handle );
echo $contents;
```
#### Using fsockopen()
```php
$fp = fsockopen( 'wordpress.org', 80, $errno, $errstr, 30 );
if (!$fp) {
  echo "$errstr ($errno)<br />\n";
} else {
  $out = "GET / HTTP/1.1\r\n";
  $out .= "Host: wordpress.org\r\n";
  $out .= "Connection: Close\r\n\r\n";
  fwrite($fp, $out);
  while (!feof($fp)) {
    echo fgets($fp, 128);
  }
  fclose($fp);
}
```
