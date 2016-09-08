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

In the script above add:
```php
...
// convert the maximum size to KB
$max = number_format(MAX_FILE_SIZE/1024, 1) . 'KB';

// create an array of permitted MIME types
$permitted = array('image/gif', 'image/jpeg', 'image/pjpeg', 'image/png');
$typeOK = false;

...

// check that file is of a permitted MIME type
foreach ($permitted as $type) {
  if ($type == $_FILES['image']['type']) {
    $typeOK - true;
    break;
  }
}

...

if ($sizeOK && typeOK) {
  switch($_FILES['image']['error']) {

...
```

#### Preventing files from being overwritten
Add a timestamp when renaming uploaded file uaing time() or date() functions:
```
 $success = move_uploaded_file($_FILES['image']['tmp_name'], UPLOAD_DIR . $time() . $filename);
```
or use IF statment to check if a file with the same email exists:
```
...
if (!file_exists(UPLOAD_DIR . $file)) {
 ...
```

#### Organizing uploads into specific folder
Use a username or any other anchors to create a specific directory. Same script as above:
```
...
  switch($_FILES['image']['error']) {
    case 0:
    // $username would normally come from a session variable
    $username = 'david';
    // if the subfolder doesn't exist yet, create it
    if (!is_dir(UPLOAD_DIR . $username)) {
      mkdir(UPLOAD_DIR . $username);
    }
  ...
```
#### Uploading multiple files
Since $_FILES is a multidimensional array, it's capable of handling multiple uploads. Update the input filel of a form:
```html
<input type="file" name="image[]" id="image1" />
```
Just use a foreach() clause to go over all file uploads:
```php
...
foreach ($_FILES['image']['name'] as $number +> $file) {
...
```

#### Complete scripts OO version
Form:
```php
<?php
// set the maximum upload size in bytes
$max = 51200;
if (isset($_POST['upload'])) {
  // define the path to the upload folder
  $destination = 'C:/upload_test/';
  require_once('../classes/Ps2/Upload.php');
  try {
	$upload = new Ps2_Upload($destination);
	$upload->move();
	$result = $upload->getMessages();
  } catch (Exception $e) {
	echo $e->getMessage();
  }
}
?>
<!DOCTYPE HTML>
<html>
<head>
<meta charset=utf-8">
<title>Upload File</title>
</head>

<body>
<?php
if (isset($result)) {
  echo '<ul>';
  foreach ($result as $message) {
	echo "<li>$message</li>";
  }
  echo '</ul>';
}
?>
<form action="" method="post" enctype="multipart/form-data" id="uploadImage">
  <p>
    <label for="image">Upload image:</label>
    <input type="hidden" name="MAX_FILE_SIZE" value="<?php echo $max; ?>">
    <input type="file" name="image" id="image">
  </p>
  <p>
    <input type="submit" name="upload" id="upload" value="Upload">
  </p>
</form>
</body>
</html>
```
Class (Upload.php)
```php
<?php
class Ps2_Upload {
	
  protected $_uploaded = array();
  protected $_destination;
  protected $_max = 51200;
  protected $_messages = array();
  protected $_permitted = array('image/gif',
								'image/jpeg',
								'image/pjpeg',
								'image/png');
  protected $_renamed = false;

  public function __construct($path) {
	if (!is_dir($path) || !is_writable($path)) {
	  throw new Exception("$path must be a valid, writable directory.");
	}
	$this->_destination = $path;
	$this->_uploaded = $_FILES;
  }

  public function getMaxSize() {
	return number_format($this->_max/1024, 1) . 'kB';
  }

  public function setMaxSize($num) {
	if (!is_numeric($num)) {
	  throw new Exception("Maximum size must be a number.");
	}
	$this->_max = (int) $num;
  }

  public function move($overwrite = false) {
	$field = current($this->_uploaded);
	if (is_array($field['name'])) {
	  foreach ($field['name'] as $number => $filename) {
		// process multiple upload
		$this->_renamed = false;
		$this->processFile($filename, $field['error'][$number], $field['size'][$number], $field['type'][$number], $field['tmp_name'][$number], $overwrite);	
	  }
	} else {
	  $this->processFile($field['name'], $field['error'], $field['size'], $field['type'], $field['tmp_name'], $overwrite);
	}
  }

  public function getMessages() {
	return $this->_messages;
  }
  
  protected function checkError($filename, $error) {
	switch ($error) {
	  case 0:
		return true;
	  case 1:
	  case 2:
	    $this->_messages[] = "$filename exceeds maximum size: " . $this->getMaxSize();
		return true;
	  case 3:
		$this->_messages[] = "Error uploading $filename. Please try again.";
		return false;
	  case 4:
		$this->_messages[] = 'No file selected.';
		return false;
	  default:
		$this->_messages[] = "System error uploading $filename. Contact webmaster.";
		return false;
	}
  }

  protected function checkSize($filename, $size) {
	if ($size == 0) {
	  return false;
	} elseif ($size > $this->_max) {
	  $this->_messages[] = "$filename exceeds maximum size: " . $this->getMaxSize();
	  return false;
	} else {
	  return true;
	}
  }
  
  protected function checkType($filename, $type) {
	if (empty($type)) {
	  return false;
	} elseif (!in_array($type, $this->_permitted)) {
	  $this->_messages[] = "$filename is not a permitted type of file.";
	  return false;
	} else {
	  return true;
	}
  }

  public function addPermittedTypes($types) {
	$types = (array) $types;
    $this->isValidMime($types);
	$this->_permitted = array_merge($this->_permitted, $types);
  }

  protected function isValidMime($types) {
    $alsoValid = array('image/tiff',
				       'application/pdf',
				       'text/plain',
				       'text/rtf');
  	$valid = array_merge($this->_permitted, $alsoValid);
	foreach ($types as $type) {
	  if (!in_array($type, $valid)) {
		throw new Exception("$type is not a permitted MIME type");
	  }
	}
  }

  protected function checkName($name, $overwrite) {
	$nospaces = str_replace(' ', '_', $name);
	if ($nospaces != $name) {
	  $this->_renamed = true;
	}
	if (!$overwrite) {
	  $existing = scandir($this->_destination);
	  if (in_array($nospaces, $existing)) {
		$dot = strrpos($nospaces, '.');
		if ($dot) {
		  $base = substr($nospaces, 0, $dot);
		  $extension = substr($nospaces, $dot);
		} else {
		  $base = $nospaces;
		  $extension = '';
		}
		$i = 1;
		do {
		  $nospaces = $base . '_' . $i++ . $extension;
		} while (in_array($nospaces, $existing));
		$this->_renamed = true;
	  }
	}
	return $nospaces;
  }

  protected function processFile($filename, $error, $size, $type, $tmp_name, $overwrite) {
	$OK = $this->checkError($filename, $error);
	if ($OK) {
	  $sizeOK = $this->checkSize($filename, $size);
	  $typeOK = $this->checkType($filename, $type);
	  if ($sizeOK && $typeOK) {
		$name = $this->checkName($filename, $overwrite);
		$success = move_uploaded_file($tmp_name, $this->_destination . $name);
		if ($success) {
			$message = "$filename uploaded successfully";
			if ($this->_renamed) {
			  $message .= " and renamed $name";
			}
			$this->_messages[] = $message;
		} else {
		  $this->_messages[] = "Could not upload $filename";
		}
	  }
	}
  }

}
```
