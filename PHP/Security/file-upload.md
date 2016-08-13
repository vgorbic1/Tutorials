#### UPLOADING FILES
Strip out the filename!
```php
<!DOCTYPE html>
<html>
  <head>
    <title>File Upload</title>
  </head>
  <body>
    <form method='post' action='fileupload.php'
        enctype='multipart/form-data'>
      Choose File: <input type='file' name='filename' size='27'>
      <input type='submit' value='Upload'>
    </form>
<?php
  if ($_FILES)
  {
    $name = strtolower(preg_replace('/[^\w.-]/', '',
      $_FILES['filename']['name']));
    move_uploaded_file($_FILES['filename']['tmp_name'], $name);
    echo "Uploaded image '$name'<br><br><img src='$name'>";
  }
?>
  </body>
</html>
```
#### uniqid()
The ```uniqid()``` function generates a unique ID based on the microtime (current time in microseconds). The generated ID from this function is not optimal, because it is based on the system time. To generate an extremely difficult to predict ID, use the md5() function.
```php
echo uniqid();
```
