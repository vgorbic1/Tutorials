## File Handling
Check if the file already exists before writing to it. 

Use file_exists() function:
```php
if (file_exists('myfile.info')) echo 'File exists';
```
This function returns TRUE if a file already exists. If no filepath specified, the function looks into the current folder. Otherwise, use a relative path:
```php
if (file_exists('../myfolder/myfile.info')) echo 'File exists';
```
Even better, use a globals array for all paths and then use one of the elements for the function:
```php
$GLOBALS['mypath'] = '/usr/home/peter/';
if (file_exists($GLOBALS['mypath'] . 'myfile.info')) echo 'File exists';
```

#### Opening and Creating A File
To open files for reading use fopen() that crates a handle. Include a mode as an argument:
```php
$filehandle = fopen('myfile.info', 'w');
```
- r opens for reading;
- r+ opens for reading and writing with the file pointer placed in the start of the file.
- w opens a file for writing only with pointer in the start. If file exists, the file size is set to 0. If file does not exist, it creates the file. On error, FALSE I returned.
- w+ opens a file for writing and reading. The rest is like with W mode.
- a opens a file for writing only with pointer at the end. The rest as with W mode.
- a+ opens for reading and writing with pointer at the end. The rest as with W mode.
- b On systems such as Windows that differentiate between text and binary files. If it is a binary data you need to included b alongside: 
```php
fopen('file', 'rb+');
```

#### Writing to A File
To write into an open file use fwrite() function with the handle of the opened file and the string to write:
```php
fwrite($filehandle, "Hello!");
```
The data is written starting at the current pointer location. You can write not only a string, but also a binary data (image for example). If it cannot write to the file, it will return FALSE, otherwise it will return the number of bytes written. Therefore, it is better to check if it succeeded:
```php
$flag = fwrite($filehandle, "Hello!");
if ($flag == FALSE) die('Fatal error: could not write to file.');
```

#### Closing a File 
To close file after accessing it use fclose() function with the handle of the opened file:
```php
fclose($filehandle);
```
This will flush any yet unwritten data to the file, close it, and the handle will be invalid. PHP closes the file automatically on program exit, but it is a good habit to close it deliberately each time you finish access to it.

#### Reading from a File
Open the file first with fopen() function with a reading mode. Read a single character with fgetc() function. It will advance the pointer by 1 and store retrieved character in $char:
```php
$char = fgetc($filehandle);
```
To read an entire line from the file to the next newline (\n) character use fgets() function. The newline character will be returned too:
```php
$line = fgets($filehandle);
```
To read the certain number of characters from the line use extra argument:
```php
$line = fgets($filehandle, 250);
```
This will read 249 characters. Check the returning data first:
```php
$line = fgets($filehandle, 250);
if ($line == FALSE) die('Fatal error: could not read from file.');
```
The same thing:
```php
$line = fgets($filehandle, 250) or die('Fatal error: could not read from file.');
```
To read binary data from a file use fread() function. It reads the number of bytes provided as an argument unless the end of file is reached:
```php
$data = fread($filehandle, 512); 
```
This will read 512 byte of the binary file. To read entire binary file use the following:
```php
$data = fread($filehandle, filesize($filename)) or die('Fatal error: could not read from file.');
```

#### Fast File Accessing
To quickly grab the contents of a file use file_get_contents() function:
```php
if (file_exists('file.txt')) {
  $mylist = @file_get_contents('file.txt') != FALSE
    or $message = 'Could not retrieve file';
}
```
You even can provide an URL to the function to read the content of the file:
```php
$image = file_get_contents('http//mysite.com/image.jpg');
```

#### File Copying
To copy a file you do not need to open, read, and write to another. Just use copy() function:
```php
copy('original.file', 'copied.file') != FALSE or die('Could not copy file');
```

#### File Deleting
To delete a file use unlink() function:
```php
if (unlinck('original.file') == FALSE) die('Could not delete file');
```

#### File Moving
Use rename() function for moving a file:
```php
rename('original.file', 'copied.file') != FALSE or die('Could not rename file');
```

#### Random Access
Using file pointer you may randomly access any character in an opened file.
To move the file pointer use fseek() function with the file handle, offset value, and optionally an argument to specify where’re the seek should be from.
Seek all the way back to the start of the file:
```php
fseek($filehandle, 0);
```
It is the same as:
```php
rewind($filehanle);
```
Add arguments:
- SEEK_SET Seeks from the file's start (default)
- SEEK_CUR Seeks from the current file pointer
- SEEK_END Seeks from the file's end

To move the pointer to the end of a file:
```php
fseek($filehandle, 0, SEEK_END);
```
Use positive or negative values when seeking from the start or from the end of the file.

To determine where the file pointer is use ftell() function:
```php
$filepointer = ftell($filehandle);
```

#### Manging Directories
To create a directory use mkdir() function. To create a directory in the current folder:
```php
mkdir('newfolder');
```
On error the function returns FALSE. 

On Unix/Linux the default file mode will be 0777 (full access for all users)

To limit access to read for all, but write by others use an argument:
```php
mkdir('newfolder', 0755);
```
To remove directory in the current folder:
```php
rmdir('newfolder');
```

#### File Locking
Use flock() function so multiple users can access the same file at the same time via queuing system.
```php
$handle = @fopen('guestbook.txt', 'a+') != FALSE 
  or die('Cannot open the file');
if (@flock($handle, LOCK_EX)) {             // Request the exclusive lock
    $flag = @fwrite($handle, $comment);      // Write to file
    @flock($handle, LOCK_UN);                // Release lock 
    if (!$flag) die('Cannot write to file'); // Must be after locking
}
@fclose($handle);
```

#### Compressing Files
Use zlib (zlib.net) to compress files on server. PHP has a build in support for zlib since version 4.3.
Start by opening a file using gzopen() function, indicating a mode. The modes are the same as those used with fopen(). Add a compression level from 1 (least compressed) to 9 (most compressed). Add f, h, and b flags to further modify the mode.
To write a compressed file:
```php
$fp = gzopen('filename.gz', 'w5');
gzwrite($fp, 'data');
gzclose($fp);
```
To read a compressed file use readgzfile() function, which reads in a compressed file, decompresses the data, and sends it to an output. Alternatively, use gzfile() function, which reads in a compressed file, decompresses it, and returns it as an array (one element for each line in the file).
Create a compressed backup of a database's records:
```php
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Database Backup</title>
</head>
<body>
<?php /*  This page retrieves all 
       * the data from a database
 *  and writes that data to a text file.
 *  The text file is then compressed
 *  using zlib.
 */
 
// Establish variables and setup:
$db_name = 'test';
// Backup directory:
$dir = "backups/$db_name";
// Make the database-specific directory "backups", if it doesn't exist.
// (Make sure it is writable or check with is_writable() function if 
// needed): 
if (!is_dir($dir)) {
    if (!@mkdir($dir)) {
        die("<p>The backup directory--$dir--could not be created.</p></body></html>");
    }
}
// Get the current time for use in all filenames:
$time = time();
// Connect to the database:
$dbc = @mysqli_connect('localhost', 'username', 'password', $db_name) OR die("<p>The database--$db_name--could not be backed up.</p></body></html>");
// Retrieve the tables:
$r = mysqli_query($dbc, 'SHOW TABLES');
// Back up if at least one table exists:
if (mysqli_num_rows($r) > 0) {
    // Indicate what is happening:
    echo "<p>Backing up database '$db_name'.</p>";   
    // Fetch each table name:
    while (list($table) = mysqli_fetch_array($r, MYSQLI_NUM)) {   
        // Get the records for this table:
        $q = "SELECT * FROM $table";
        $r2 = mysqli_query($dbc, $q);        
        // Back up if records exist:
        if (mysqli_num_rows($r2) > 0) {
            // Attempt to open the file:
            if ($fp = gzopen("$dir/{$table}_{$time}.sql.gz", 'w9')) {       
                // Fetch all the records for this table:
                while ($row = mysqli_fetch_array($r2, MYSQLI_NUM)) {
                    // Write the data as a comma-delineated row:
                    foreach ($row as $value) {
                        $value = addslashes($value); //in case the data
                                              // in $value has apostrophe
                        gzwrite ($fp, "'$value', ");
                    }
                    // Add a new line to each row:
                    gzwrite ($fp, "\n"); 
                } // End of WHILE loop.
                // Close the file:
                gzclose ($fp); 
                // Print the success:
                echo "<p>Table '$table' backed up.</p>";
            } else { // Could not create the file!
                echo "<p>The file--$dir/{$table}_{$time}.sql.gz--could not be opened for writing.</p>";
                break; // Leave the WHILE loop.
            } // End of gzopen() IF.
        } // End of mysqli_num_rows() IF.   
    } // End of WHILE loop.
} else {
    echo "<p>The submitted database--$db_name--contains no tables.</p>";
} ?>
</body>
</html>
```
Now, we create a cron service to make this backup run with a set schedule:
To edit crontab manually in command-line:
```
crontab –e
```
To establish a cron for a PHP file:

Access cron jobs interface on the remote server.
Test the command on a command prompt using real place on the server where file resides:
```
curl http://localhost/db_backup.php
```
View the current contents of the crontab file:
```
crontab –l
```
Make a backup of the crontab file just in case something goes wrong.
Create a new document in your text editor or IDE:
```
1 0 * * 5 curl http://localhost/db_backup.php
```
Make sure that you press Enter(Return) once at the end of the line. We are telling chron that cURL should be invoked with that URL every Friday (5) at 12:01 a.m.
Each task should be on its own line. Save file as cronjob1 with no extension and upload it to the server in a convenient location.
With the server command prompt enter:
```
crontab /path/to/cronjob1
```
For example, the cronjob1 file may be in the Desktop folder: 
```
crontab ~/Desktop/cronjob1
```
Confirm the crontask list:
```
crontab –l
```
The crontab is unique for each user on the server.
