## File Handling

####Writing to file:
Name the file ```WriteToFile.php``` Define the class:
```php
class WriteToFile {    
    // For storing the file pointer:
    private $_fp = NULL;  
  
    // Constructor opens the file for writing:
    function __construct($file) {    
        // Check that the file exists and is a file:
        if (!file_exists($file) || !is_file($file)) {
            throw new Exception('The file does not exist.');
        }       
        // Open the file:
        if (!$this->_fp = @fopen($file, 'w')) {
            throw new Exception('Could not open the file.');
        }   
    } // End of constructor.
    
    // This method writes data to the file:
    function write($data) {
        // Confirm the write:
        if (@!fwrite($this->_fp, $data . "\n")) {
            throw new Exception('Could not write to the file.');
        }
    } // End of write() method.
    
    // This method closes the file:
    function close() {  
        // Make sure it's open:
        if ($this->_fp) {
            fclose($this->_fp);
            $this->_fp = NULL;
        }      
    } // End of close() method.

    // The destructor calls close(), just in case:
    function __destruct() {
        $this->close();
    } // End of destructor.    
} // End of WriteToFile class.
```
To use the writer:
```php
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<title>Handling Exceptions</title>
	<link rel="stylesheet" href="style.css">
</head>
<body>
	<?php 
	// Load the class definition:
	require('WriteToFile.php');
	// Start the try...catch block:
	try {    
	    // Create the object:
	    $fp = new WriteToFile('data.txt');
	    // Write the data:
	    $fp->write('This is a line of data.');
	    // Close the file:
	    $fp->close();
	    // Delete the object:
	    unset($fp);
	    // If we got this far, everything worked!
	    echo '<p>The data has been written.</p>';
	} catch (Exception $e) {
	    echo '<p>The process could not be completed because the script: ' . $e->getMessage() . '</p>';
	}
	echo '<p>This is the end of the script.</p>';
	?>
	</body>
	</html>
```
Writing to file with extended exceptions:
```php
class FileException extends Exception {
    // For returning more detailed error messages:
    function getDetails() {
        // Return a different message based upon the code:
        switch ($this->code) {
            case 0:
                return 'No filename was provided';
                break;
            case 1:
                return 'The file does not exist.';
                break;
            case 2:
                return 'The file is not a file.';
                break;
            case 3:
                return 'The file is not writable.';
                break;
            case 4:
                return 'An invalid mode was provided.';
                break;
            case 5:
                return 'The data could not be written.';
                break;
            case 6:
                return 'The file could not be closed.';
                break;
            default:
                return 'No further information is available.';
                break;
        } // End of SWITCH.  
    } // End of getDetails() method.
    
} // End of FileException class.
```
```php
class WriteToFile {   
    // For storing the file pointer:
    private $ = NULL;
    // For storing an error message:
    private $_message = '';
 
    // Constructor opens the file:
    function __construct($file = null, $mode = 'w') {
        // Assign the file name and mode
        // to the message attribute:
        $this->_message = "File: $file Mode: $mode";
        // Make sure a file name was provided:
        if (empty($file)) throw new FileException($this->_message, 0);
        // Make sure the file exists:
        if (!file_exists($file)) throw new FileException($this->_message, 1);
        // Make sure the file is a file:
        if (!is_file($file)) throw new FileException($this->_message, 2);
        // Make sure the file is writable, when necessary
        if (!is_writable($file)) throw new FileException($this->_message, 3);
        // Validate the mode:
        if (!in_array($mode, array('a', 'a+', 'w', 'w+'))) throw new FileException($this->_message, 4);
        // Open the file:
        $this->_fp = fopen($file, $mode);
    } // End of constructor.
    
    // This method writes data to the file:
    function write($data) {
        // Confirm the write:
        if (@!fwrite($this->_fp, $data . "\n")) throw new FileException($this->_message . " Data: $data", 5);
    } // End of write() method.
    
    // This method closes the file:
    function close() {
        // Make sure it's open:
        if ($this->_fp) {
            if (@!fclose($this->_fp)) throw new FileException($this->_message, 6);
            $this->_fp = NULL;
        }   
    } // End of close() method.

    // The destructor calls close(), just in case:
    function __destruct() {
        $this->close();
    } // End of destructor.
    
} // End of WriteToFile class.
```
To use the writer:
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Extending Exceptions</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<?php 
// Load the class definition:
require('WriteToFile.php');
// Start the try...catch block:
try {   
    // Create the object:
    $fp = new WriteToFile('data.txt', 'w');  
    // Write the data:
    $fp->write('This is a line of data.');   
    // Close the file:
    $fp->close();   
    // Delete the object:
    unset($fp);
    // If we got this far, everything worked!
    echo '<p>The data has been written.</p>';
} catch (FileException $e) {
    echo '<p>The process could not be completed. Debugging information:<br>' . $e->getMessage() . '<br>' . $e->getDetails() . '</p>';
}
echo '<p>This is the end of the script.</p>';
?>
</body>
</html>
```
