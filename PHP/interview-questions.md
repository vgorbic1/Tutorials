## Interview Questions

**What is the difference between $message and $$message?**

This $$message treats '$message' as its value. It is called variable variable, and (I believe) rarely used.

**What are the differences between require and include, include_once?**

- `require()` will stop executing code if it fails to find the required chunk of code.
- `include()` will still allow script to run if there is no chunk of conde to include.
- `include_once()` will include the chunk of code only once and ignore any following references to this code chunk.

**What is meant by nl2br()?**

This function replaces all newlines (\n) with HTML <br> element in the given string

**How can we encrypt the username and password using php?**
- Use MD5 function: md5("password");
- Use SHA1 function: sha1("password");

**What is the functionality of the function strstr and stristr?**
- `strstr()` looks for the first occurrence of the given parameter inside given string and return the rest: ```strstr('I found a perfect job!', 'perfect' );  // will return perfect job!```
- `stristr()` is basically the same, but case-insensitive: ```stristr('I found a perfect job!', 'PERFECT' );   // will return perfect job!```

**What is the functionality of the function htmlentities?**

This function is used to convert some characters to HTML. Used to sanitize strings: ```htmlentities('<>');  // will return &lt;&rt```

**What is the difference between the functions unlink and unset?**

`unlink()` deletes the file, `unset()` clears the content of the file.

**How can we register the variables into a session?**

Several ways. The easiest can be like this: 
```php
session_start();
$username=$_GET['username'];
session_register('username');
```

**What is the maximum size of a file that can be uploaded using php and how can we change this?**

Check upload_max_filesize in the php.ini.

**How can we increase the execution time of a PHP script?**

Use `set_time_limit(0);` where 0 means maximum time.

**How can we know the count/number of elements of an array?**

Use `count();` to get the number of elements of an array:
```php
$myArray = [0, 1, 2];
echo( count($myArray));
```

**How can we find the number of rows in a resultset?**

Use `mysqli_num_rows();`

**How can we know the number of days between two given dates?**
```php
$date = new DateTime("2016-02-03"); 
$anotherDate = new DateTime("2016-03-03"); 
$result = $anotherDate->diff($date)->format("%a");
echo $result;
```

**What are the differences between mysql_fetch_array(), mysql_fetch_object(), mysql_fetch_row()?**
- `mysql_fetch_array()` returns associative and numerical array of strings that corresponds to the fetched row.
- `mysql_fetch_row()` returns an numerical array of strings that corresponds to the fetched row.
- `mysql_fetch_object()` returns a result raw as an object.

**How can I get only the name of the currently executing file?**
```php
echo __FILE__;
```
