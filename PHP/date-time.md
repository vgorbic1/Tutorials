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
echo $now->format('Y-m-d H:i:s'); // MySQL datetime format
echo $now->getTimestamp();  
```
and with custom formatting (introduced in PHP 5.3):
```php
$input = '10/11/12';
$date = \DateTime::createFromFormat("d/m/y", $input);
echo $date->format('Y-m-d H:i:s');
```

#### DateTime Comparisons
The ```DateTime``` class handles the tricky conversions needed to compare across timezones for us:
```php
$date = new \DateTime("2014-05-31 1:30pm EST");
$timezone = new \DateTimeZone("Europe/Amsterdam");
$date2 = new \DateTime("2014-05-31 *:30pm", $timezone);

if ($date == $date2) {
  echo "These dates are the same date/time":
}
```

#### DateTime Math
Use ```DateTime->modify()``` to perform date math:
```php
$date = new \DateTime();
$date->modify("+1 month");
echo $date->format('Y-m-d H:i:s');
```
Use ```DateInterval()``` to set a specific intrval for math with ```add()``` or ```sub``` helpers:
- P38D is 38 days
- P1Y3M4D is 1 year, 3 months, 4 days
- PT45M is 45 minutes
- P1WT1H is 1 week, 1 hour
Always start with "P" and separate time from date with "T".
```php
$date = new \DateTime();
$interval = new \DateInterval('P1Y3M4DT45M');
$date->add($interval);
echo $date->format('Y-m-d H:i:s');

$date = new \DateTime();
$date->sub($interval);
echo $date->format('Y-m-d H:i:s');
```

#### Difference Between Dates
Use ```dif()``` to get difference between two ```DateTime``` objects, which returns a ```DateInterval``` object:
```php
$dave =  new \DateTime("1984-05-31 00:00", new \DateTimeZone("Europe/London"));
$jim = new \DateTime("2004-08-01 00:00", new \DateTimeZone("America/Chicago"));
$dave->diff($jim);

$difference = $dave->diff($jim);
// display difference in years
echo $difference->y;
```
If ```DateInterval``` is negative, the "invert" key will be set to 1.

#### Good old way to format date
American formatting
```php
echo date('l, F jS, Y');
```
European formatting
```php
echo date('l, jS F Y');
```
