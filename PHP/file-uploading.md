## File Uploading

Check whether your server supports uploads
```php
<?php phpinfo(); ?>
```
find ```file_uploads``` section.
- **max_execution_time** is the maximum number of seconds that a PHP script can run. If the script takes longer, PHP generates a fatal error. (Default 30)
- **max_input_time** is the maximum number of seconds thata PHP script is allowed to parse the $_POST and $_GET arrays, and file uploads. Very large uploads are likely to run out of time. (Default 60)
- **post_max_size** is the maximum permitted size of all _$POST data, including file uploads. (Default 8M)
- **upload_tmp_dir** is where PHP stores uploaded files until your script moves them to a permanent location. If no value is defined in php.ini, PHP uses the system default temporary directory.
- **upload_max_filesize** the maximum permitted size of a single upload file. (Default 2M)

Add a file upload field to a form
```html
<form action="" method="post" enctype="multipart/form-data" name="uploadImage" id="uploadImage">
  <p>
    <label for="image">Upload image:</label>
    <input type="file" name="image" id="image" />
  </p>
  <p>
    <input type="submit" name="upload" id="upload" value="Upload" />
  </p>
</form>
```
Safari does not allow direct filename input!

#### $_FILES array
To test upload array use this script after the form:
```php
</form>
<pre>
 <?php
    if (array_key_exists('upload', $_POST)) {
		print_r($_FILES);
	}
  ?>
</pre>
```
If you don't do anything with the uploaded file immediately after uploading, PHP discards it.

It is important to checkthe MIME type before allowing the upload process to be completed.

**Errors**

- 0 Upload successful
- 1 File exceeds maximum upload size specified in php.ini
- 2 File exceeds size specified by MAX_FILE_SIZE embedded in the form
- 3 File only partially uploaded
- 4 Form submitted with no file specified
- 5 (Currently not defined)
- 6 No temporary folder
- 7 Cannot write file to disk

In most cases PHP runs as *nobody* or "appache* username, so you have to have proper permissions to upload files in your upload directory. Place download directory in a private directory on the server.

Move downloaded file from temporary directory to your download directory with ```move_uploaded_file()```. Becaulse the second argument of this function requires a full pathname, it gives you the opportunity to rename the file!

#### Uploading Script
Using the form names from the form above:
```php
<?php
if (array_key_exists('upload', $_POST)) {
  
  // define constant for upload folder
  define('UPLOAD_DIR', '/absolute/path/to/upload/directory/');
  
  //move the file to the upload directory and rename it
  move_uploaded_file($_FILES['image']['tmp_name'], UPLOAD_DIR . $_FILES['image']['name']);
}
?>
```
If the file of the same name already exists in the upload directory, the new file will overwrite it without warning. There are some techniques to prevent this from happening. 

Do not use ```copy()``` instead of ```move_uploaded_file()``` because of security reasons!

#### Remove spaces from filenames
```php
...
define('UPLOAD_DIR', '/absolute/path/to/upload/directory/');
$filename = str_replace(' ', '_', $_FILES['image']['name']);
 move_uploaded_file($_FILES['image']['tmp_name'], UPLOAD_DIR . $filename);
 ```
 
 #### Rejecting large files
 Add the following in the form before the file input field:
 ```php
 <input type="hidden" name="MAX_FILE_SIZE" value=<?php echo MAX_FILE_SIZE; ?>" />
```
Define the size of the file in the top of your PHP download script:
```php
define('MAX_SIZE', 3000); // in bytes
```
Check the file size in PHP script:
```php
...
$filename = str_replace(' ', '_', $_FILES['image']['name']);

// convert the maximum size to KB
$max = number_format(MAX_FILE_SIZE/1024, 1) . 'KB';
$sizeOK =  false;

// check that file is within the permitted size
if ($_FILES['image']['size'] > 0 && $_FILES['image']['size'] <= MAX_FILE_SIZE) {
  $sizeOK = true;
}

if ($sizeOK) {
  switch($_FILES['image']['error']) {
    
    case 0:
      // move file to the upload directory and renamet it
      $success = move_uploaded_file($_FILES['image']['tmp_name'], UPLOAD_DIR . $filename);
      if ($success) {
        $result = "$file uploaded successfully";
      } else {
        $result = "Error uploading $file. Please try again.";
      }
      break;
    
    //case 1: and case 2: (maximum size) is alreadey taken care of 
    
    case 3:
      $result = "Error uploading $file. Please try again.";
    
    // tacking care or errors 6 and 7
    default:
      $result = "System error uploading $file.";
    }
  
  } elseif ($_FILES['image']['error'] == 4) {
    $result = "No file selected";
  } else {
    $result = "$file cannot be uploaded. Maximum size: $max.";
  }
}
```

#### Accepting only certain types of files
- application/msword
- application/pdf
- text/plain
- text/rtf
- image/gif
- image/jpeg
- image/pjpeg (JPEG format, nonstandard MIME type used by IE)
- image/png
- image/tiff
