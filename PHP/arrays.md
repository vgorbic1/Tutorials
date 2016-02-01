## Arrays
Arrays are collections of data.

#### Creating arrays
```PHP
$myArray = array();
  // or
$myArray = array(123, "Hello!", 3.21);
  // or
$myArray = [];
```

#### Assigning values
```PHP
$myArray[0] = 123;
$myArray[1] = "Hello!";
$myArray[2] = $OtherArray;
$myArray[] = 12.34;
$myArray[$myIndex] = "Hi";
$myArray[$otherArray[0]] = "Hey!";
```
#### Retrieving values
```PHP
echo $MyArray[0];
```

#### Creating associative arrays
Use a string as a key for an element to form a Hash Table:
```PHP
$soccerTeam = array();
$soccerTeam['Andy'] = 1;
$soccerTeam['Brian'] = 2;
  // or
$soccerTeam = array('Andy' => 1, 'Brian' => 2);
  // or
$soccerTeam = ['Andy' => 1, 'Brian' =>2];
```

#### Multidimensional arrays
There are no such thing as multidimensional arrays in PHP. Just simulate it using normal arrays.
```PHP
$myTable0 = array(1, 2);
$myTable1 = array(3, 4);
$masterTable = array($myTable0, $myTable1);
```
To assign values:
```PHP
echo $MasterTable[0][0];
```

#### Multidimensional associative arrays:
```PHP
$rattle = array('price' => 2.99, 'stock' => 3);
$bear = array('price' => 3.99, 'stock' => 5);
  $pacifier = array('price' => 1.99, 'stock' => 10);
  $dolly = array('price' => 4.99, 'stock' => 6);
      $baby = array('rattle' => $rattle, 'bear' => $bear);
      $toddler = array('pacifier' => $pacifier, 'dolly' => $dolly); 
          $products = array('baby' => $baby, 'toddler' => $toddler);
```
To access them use:
```PHP
echo $products['baby']['rattle']['price']  // result is 2.99
```

#### Array Functions
**foreach()**

This function allows iterating through an array one element at a time
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
foreach($cats as $cat)  echo "$cat<br />";

// or for associative array:
$soccerTeam = array('Andy' => 1, 'Brian' => 2);
foreach($socerTeam as $player => $number) echo "$player has number $number";
```

**array_merge()**

This function returns a new array created by joining two other arrays together. The original arrays are not changed in any way, only result of joining them is returned.
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
$dogs = array('Pit Bull', 'Spaniel', 'Terrier');
$pets = array_merge($cats, $dogs);
```

**implode()** or **join()**

This function turns all elements in an array into a string. 
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
echo implode(' and ', $Cats); // this will give you a sting: Long Hair and Short Hair and Dwarf
```

**array_walk()**

This function processes all the elements of given array passing to the function as an argument:
```PHP
$nums = array(99, 16, 11);
array_walk($nums, 'CalcRoot'); 
function calcRoot ($item){    
    echo "Root $item is " . sqrt($item);
}
```

**size_off()**

This function tells you how many elements in the current array
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
echo sizeof($Cats); // result is 3.

//To add a new element to the end of the array:
$cats[sizeof($cats)] = 'Siamese';
```

**array_push()**

This function helps to add an element to the end of an array.
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
array_push($cats, 'Siamese');
```

**array_pop()**

This function removes the last element from an array.
```PHP
array_pop($myArray);

// To remove the last element and store it in a variable:
$myVariable = array_pop($myArray);
```

**array_reverse()**

This function reverses the order of elements in an array.
```PHP
$myArray = array_reverse($myArray);
```

**array_flip()**

This function returns a new array where key/value pairs are reversed. The key and values must be integers or strings.
```PHP
$myArray = array('One' => 1, 'Two' => 2);
$flippedArray = array_flip($myArray); // results in array (1 => 'One', 2 => 'Two');
```

#### FILO and FIFO Arrays
First In, Last Out Arrays. Also called a stack. (Sometimes called LIFO)

First In, First Out Arrays. Also called a buffer. Used for handling events such as keyboard input. (Sometimes called LILO)

**array_unshift()**

This function inserts new element in the beginning of the array.
```PHP
$myArray = array(99, 16, 11);
array_unshift($myArray, 33);  // now array has 33, 99, 16, 11.
```

**array_splice()**

This function helps to insert, remove, or replace any element in a given array.
To remove an element:
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf', 'Siamese');
array_splice($cats, 1, 2); // now array has Long Hair, Siamese. It start with position 1 (0 counts too) and take 2 elements away.
```
To see which elements were taken:
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf', 'Siamese');
$elementsRemoved = array_splice($cats, 1, 2);
echo $elementsRemoved;
```
To insert elements into an array:
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf', 'Siamese');
array_splice($cats, 2, 0, 'Persian'); // now array has Long Hair, Short Hair,  Persian, Dwarf, Siamese. Start inserting in position 1 (0 counts too), do not remove anything, but add ‘Persian’.
```
To replace element:
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf', 'Siamese');
array_splice($cats, 2, 1, 'Persian');  // now arrays has Long Hair, Short Hair, Persian, Siamese. Remove 1 element at position 2 (0 counts too) and insert string ‘Persian’ there.
```

#### Soring arrays

**sort()**

This function sorts array elements alphabetically and case sensitively in ascending order. This function changes the original array! 
```PHP
$cats = array('Long Hair', 'Short Hair', 'Dwarf');
sort($cats); // now array has Dwarf, Long Hair, Short Hair.
```
To change the numerical order use SORT_NUMERIC parameter:
```PHP
$nums = array(99, 16, 11);
sort($nums, SORT_NUMERIC); // now array has 11, 16, 99
```

*Other Sorting functions:*
- rsort() - sort arrays in descending order.
- asort() - sort associative arrays in ascending order, according to the value.
- ksort() - sort associative arrays in ascending order, according to the key.
- arsort() - sort associative arrays in descending order, according to the value.
- krsort() - sort associative arrays in descending order, according to the key.

#### Sorting multidimensional arrays
To sort a multidimensional array, you define your own sort function and then tell PHP to use that function by invoking the built-in sort functions:
```PHP
$students = array(
	256 => array('name' => 'Jon', 'grade' => 98.5),
	2 => array('name' => 'Vance', 'grade' => 85.1),
	9 => array('name' => 'Stephen', 'grade' => 94.0),
	364 => array('name' => 'Steve', 'grade' => 85.1),
	68 => array('name' => 'Rob', 'grade' => 74.6));

// Name sorting function:
function name_sort($x, $y) {
	return strcasecmp($x['name'], $y['name']);
}

// Grade sorting function:
// Sort in DESCENDING order!
function grade_sort($x, $y) {
	return ($x['grade'] < $y['grade']);
}

// Print the array as is:
echo '<h2>Array As Is</h2><pre>' . print_r($students, 1) . '</pre>';

// Sort by name:
uasort($students, 'name_sort');
echo '<h2>Array Sorted By Name</h2><pre>' . print_r($students, 1) . '</pre>';

// Sort by grade:
uasort($students, 'grade_sort');
echo '<h2>Array Sorted By Grade</h2><pre>' . print_r($students, 1) . '</pre>';
```
