## Dates and Times
Beginning with PHP 5.1 a default timezone identifier should be set.

Use either ```date_default_timezone_set(*timezone-identifier*) in PHPH script, or ```date.timezone``` in php.ini.

PHP 5.2 introduced the ```DateTime``` class to simplify working with dates and times.

PHP 5.5 introduced ```DateTimeImmutable``` class that returns a new instance of that class when making modifications, rather than modifying and returning ```itself($this)```.

```DateTime``` is recomended over older functions for working with dates and times. Use ```microtime()``` to work with times. 

#### Datetime construction
Prefixing DateTime with a \ ensures we're using the class from the global namespace.
```php
// Current time
$date = new \DateTime();
 or
$date = new \DateTime("now");

// June 18th, 2014, at 2:05pm
// Eastern Time (Daylight savings count)
$date = new \DateTime("2014-06-18 14:05 EST");

// Current time, yesterday
$date = new \DateTime("yesterday");

// Current time, two days ago
$date = new \DateTime("-2 days");
```
Specify timezone as a second argument to adjust to the local time:
```php
$timezone = new \DateTimeZone("Europe/London");
$date = new \DateTime("3 weeks ago", $timezone);
```

#### Retrieving a Date/Time
Use ```DateTime -> format()``` method with the same traditional ```date()``` valueds. It returns a string.
```php
$now = new DateTime();
echo $now->format('Y-m-d H:i:s');    // MySQL datetime format
echo $now->getTimestamp();  
```
and with custom formatting (introduced in PHP 5.3):
```php
$input = '10/11/12';
$date = \DateTime::createFromFormat("d/m/y", $input);
```




#### Formatted date
American style
```php
echo date('l, F jS, Y');
```
European style
```php
echo date('l, jS F Y');
```
