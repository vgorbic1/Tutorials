## JSON
While XML used to be the format of choice for many systems, it has been surpassed by JSON, which is supported by many languages.

To work with JSON in PHP you need the following functions:
* `json_encode()` (to return the JSON representation of a value)
* `json_decode()` (to decode a JSON string)
* `json_last_error()` (to return the last error occured)

#### Encoding JSON
PHP `json_encode()` function is used for encoding JSON in PHP. This function returns the JSON representation of a value on success or FALSE on failure. This function only works with UTF-8 encoded data.
```PHP
<?php
   $arr = array('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
   echo json_encode($arr);
?>
```
returns the JSON string:
```javascript
{ "a":1,
  "b":2,
  "c":3,
  "d":4,
  "e":5 }
```
To convert an object to JSON string:
```PHP
   class Employee {
      public $name = "";
      public $hobbies  = "";
      public $birthdate = "";
   }
	
   $e = new Employee();
   $e->name = "James";
   $e->hobbies  = "sports";
   $e->birthdate = date('m/d/Y h:i:s a', "8/5/1974 12:20:03 p");
   $e->birthdate = date('m/d/Y h:i:s a', strtotime("8/5/1974 12:20:03"));

   echo json_encode($e);
```
returns the JSON string:
```javascript
{ "name":"James",
  "hobbies":"sports",
  "birthdate":"08\/05\/1974 12:20:03 pm" }
```
or
```php
class User implements JsonSerializable {
  public $first_name;
  public $last_name;
  public $email;
  public $password;
  
  public function jsonSerialize() {
    return [
      "name => $this->first_name . ' ' . $this->last_name, 
      "email_hash" => md5($this->email),
    ];
  }
}

$User =  new User();
echo json_encode($User);
```
results in:
```
{
  "name": "blah-blah",
  "email_hash": "c1dqdkee94kt88wkd9w0ut"
}
```

**More Examples:**
```PHP
$arr = array(
    array(
        "region" => "valore",
        "price" => "valore2"
    ),
    array(
        "region" => "valore",
        "price" => "valore2"
    ),
    array(
        "region" => "valore",
        "price" => "valore2"
    )
);

echo json_encode($arr);
```
returns the JSON string:
```javascript
{"region":"valore","price":"valore2"},
{"region":"valore","price":"valore2"},
{"region":"valore","price":"valore2"}
```
Example with arrays:
```PHP
$obj = new stdClass();
$obj->label="Devices per year";
$obj->data = array(
    array('1999','3.0'),
    array('2000','3.9'),
);

echo json_encode($obj);
```
returns the JSON string:
```javascript
{ 
    "label": "Devices per year",
    "data": [
        [1999, 3.0], [2000, 3.9]
    ]
}
```
In PHP 5.3 several options for the ```jason_encode()``` were introduced. For example:
```php
$array = ["name => "John Doe", "age" => "30"];
$options = JSON_PRETTY_PRINT | JSON_NUMERIC_CHECK | JSON_FORCE_OBJECT;
echo json_encode($array, $options);
```
will produce:
```
{
  "name": "John Doe",
  "age": 30
}
```
In PHP 5.5 a third parameter ```depth``` was added to limit how many nested data structures will be encoded.

#### Decoding JSON
PHP `json_decode()` function is used for decoding JSON in PHP. This function returns the value decoded from json to appropriate PHP type. 
```PHP
   $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

   var_dump(json_decode($json));
   var_dump(json_decode($json, true)); // add true to return an array
```
this will echo out:
```
object(stdClass)#1 (5) {
   ["a"] => int(1)
   ["b"] => int(2)
   ["c"] => int(3)
   ["d"] => int(4)
   ["e"] => int(5)
}

array(5) {
   ["a"] => int(1)
   ["b"] => int(2)
   ["c"] => int(3)
   ["d"] => int(4)
   ["e"] => int(5)
}
```
Yo can specify ```depth`` and ```options``` as the third and forth arguments. ```JSON_BIGINT_AS_STRING``` is the only option that is supported.
