## HTTP Requests with PHP
Depending on the server setup and configuration, PHP version, or security
settings, some methods won’t be allowed or even available.
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
#### Using the CURL expression
```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "http://wordpress.org/");
curl_setopt($ch, CURLOPT_HEADER, 0);
curl_exec($ch);
curl_close($ch);
```
