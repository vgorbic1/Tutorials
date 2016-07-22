##Sessions
By default, PHP stores all session data in text files in the server in a temporary folder with filenames matching the session IDs. To improve security, store the session data in a database, which also allows to store more info about sessions. Another improvement is ability to use the same session data fed from different servers.

To store session data use a separate table on a database. The table has to have at least three columns:
```sql
CREATE TABLE sessions (id CHAR(32) NOT NULL, data TEXT, last_accessed 
    TIMESTAMP NOT NULL, PRIMARY KEY (id));
```
Next, define the functions for interacting with the database and tell PHP to use those functions.
Every time a session is started, the "open" and "read" functions are calledautomaically and immediately. When the "read" function is called, garbage collection may take place. When a script terminates, the "write" function is called, and then the "close" function is called. If the session is destroyed, the "write" function is not called, but "destroy" function will be, followed by "close" function.
```php
<?php # Script 3.1 - db_sessions.inc.php
/* 
 *  This page creates the functional interface for 
 *  storing session data in a database.
 *  This page also starts the session.
 */
// Global variable used for the database 
// connections in all session functions:
$sdbc = NULL;

// Define the open_session() function:
// This function takes no arguments.
// This function should open the database connection.
// This function should return true.
function open_session() {
    global $sdbc;  
    // Connect to the database:
    $sdbc = mysqli_connect ('localhost', 'username', 'password', 'test');
    return true;
} // End of open_session() function.
 
// Define the close_session() function:
// This function takes no arguments.
// This function closes the database connection.
// This function returns the closed status.
function close_session() {
    global $sdbc;
    return mysqli_close($sdbc);
} // End of close_session() function.

// Define the read_session() function:
// This function takes one argument: the session ID.
// This function retrieves the session data.
// This function returns the session data as a string.
function read_session($sid) {
    global $sdbc;
    // Query the database:
    $q = sprintf('SELECT data FROM sessions WHERE id="%s"', mysqli_real_escape_string($sdbc, $sid)); 
    $r = mysqli_query($sdbc, $q);    
    // Retrieve the results:
    if (mysqli_num_rows($r) == 1) {
        list($data) = mysqli_fetch_array($r, MYSQLI_NUM);
        return $data;
    } else { // Return an empty string.
        return '';
    }
} // End of read_session() function.

// Define the write_session() function:
// This function takes two arguments: 
// the session ID and the session data.
function write_session($sid, $data) {
    global $sdbc;
    // Store in the database:
    $q = sprintf('REPLACE INTO sessions (id, data) VALUES ("%s", "%s")', mysqli_real_escape_string($sdbc, $sid), mysqli_real_escape_string($sdbc, $data)); 
    $r = mysqli_query($sdbc, $q);
	return true;
} // End of write_session() function.

// Define the destroy_session() function:
// This function takes one argument: the session ID.
function destroy_session($sid) {
    global $sdbc;
    // Delete from the database:
    $q = sprintf('DELETE FROM sessions WHERE id="%s"', mysqli_real_escape_string($sdbc, $sid)); 
    $r = mysqli_query($sdbc, $q); 
    // Clear the $_SESSION array:
    $_SESSION = array();
    return true;
} // End of destroy_session() function.

// Define the clean_session() function:
// This function takes one argument: a value in seconds.
function clean_session($expire) {
    global $sdbc;
    // Delete old sessions:
    $q = sprintf('DELETE FROM sessions WHERE DATE_ADD(last_accessed, INTERVAL %d SECOND) < NOW()', (int) $expire); 
    $r = mysqli_query($sdbc, $q);
    return true;
} // End of clean_session() function.

# ***** END OF FUNCTIONS ***** #

// Declare the functions to use:
session_set_save_handler('open_session', 'close_session', 'read_session', 'write_session', 'destroy_session', 'clean_session');

// Make whatever other changes to the session settings, if you want.
// Start the session:
session_start();
```
Include this script to every page that needs session tracking.

The following code demonstrates how to use this mechanism:
```php
<?php # Script 3.2 - sessions.php
/*  This page does some silly things with sessions.
 *  It includes the db_sessions.inc.php script
 *  so that the session data will be stored in a database.
 */ 
// Include the sessions file:
// The file already starts the session.
require('db_sessions.inc.php');
?><!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>DB Session Test</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<?php
// Store some dummy data in the session, if no data is present:
if (empty($_SESSION)) {

    $_SESSION['blah'] = 'umlaut';
    $_SESSION['this'] = 3615684.45;
    $_SESSION['that'] = 'blue';
    
    // Print a message indicating what's going on:
    echo '<p>Session data stored.</p>';
    
} else { // Print the already-stored data:
    echo '<p>Session Data Exists:<pre>' . print_r($_SESSION, 1) . '</pre></p>';
}

// Log the user out, if applicable:
if (isset($_GET['logout'])) {

    session_destroy();
    echo '<p>Session destroyed.</p>';
    
} else { // Otherwise, print the "Log Out" link:
    echo '<a href="sessions.php?logout=true">Log Out</a>';
}

// Reprint the session data:
echo '<p>Session Data:<pre>' . print_r($_SESSION, 1) . '</pre></p>';

// Complete the page:
echo '</body>
</html>';

// Write and close the session:
session_write_close(); 
?>
```
-Taken from "PHP Advanced and Object-Oriented Programming" by Larry Ullman
