## JSON
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

#### Decoding JSON
PHP `json_decode()` function is used for decoding JSON in PHP. This function returns the value decoded from json to appropriate PHP type. 
```PHP
   $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

   var_dump(json_decode($json));
   var_dump(json_decode($json, true));
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
