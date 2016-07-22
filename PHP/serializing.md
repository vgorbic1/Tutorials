## Serializing
Serializing of objects, which is a conversion of complex data type (found in objects or arrays) into a primitive data type using serialize() function in order to store the data in session or a database.

#### ARRAYS
```php
$data = array('Karen' => 'Toronto', 'Stephanie' => 'Boston', 'Jessica' => 'State College');
$sData = serialize($data);
```
Now, $sData would have a string with value of:
```php
a:3:{s:5:"Karen";s:7"Toronto";s:9:"Stephanie";s:6:"Boston";s;7:"Jessica";s:13:"Stage College";}
```
Saying that the data is an array, consiting of three elemens. The first element uses a string for its key, containing five characters, with the value of Karen. That element has a string for its value, containing seven characters, with a value of Toonto. And so on.

#### OBJECTS
The process is the same with objects, but a serialized object will only store the values of the object's attributes, along with the name of the object's class. The object methods will not be stored. 
PHP needs access to the object's class definition in order to re-create the object. As long as PHP can do that, the original object will be properly reconstituted, retaining its attribute values and able to invoke its methods once again.
If you are storing an object in a session, PHP will automaically seialize and unserialize the data on the fly. The PHP just needs to access the corresponding class definitions when the session is started again.

#### UNSERIALIZING
From  that string, the data can be reconstituted into its complex format via the ```unserialize()``` function:
```php
$data = unserialize($sData);
```
