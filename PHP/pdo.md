## PDO
PHP Data Objects

#### CONNECTING TO A DATABASE
PDO is an alternative way to interact with a database, regardless of the application in use. PDO works with MySQL, PostgreSQL, SQLite, Oracle, Microsoft SQL Server, and more. PHP has to have PDO extension enabled and you have to have a driver for the certain database application you are going to use.
To confirm what applications are supported:
```php
print_r(PDO::getAvailableDrivers());
```
Connect to database:
```php
$pdo = new PDO('dsn', 'username', 'password');
```
'dsn' means Data Source Name (DSN) and is a string that indicates:
-	The database driver to use
-	The database name
-	In the case of SQLite, the location of the database file
-	Optionally the host name
-	Optionally the port

It is possible to include username and password to the DSN too.

To create the DSN, locate the database driver. After a colon, use name=value pairs separated by a semicolon:

To connect to MySQL:
```php
$pdo = new PDO('mysql:dbname=test; host=localhost', 'username', 'password');
```
To connect to SQLite:
```php
$pdo = new PDO('sqlite:/path/to/somedb.sq3);
```
SQLite connects via specific files and do not require usernames and passwords.

PHP will automatically close the connection after script terminates, but it makes for good form.

To close the connection use:
```php
unset($pdo); 
```
or set it to null:
```php
$pdo = null;
```

To handle database-related errors that might occur when using PDO, write exception blocks. PDO throws exceptions of type PDOException. To interact with database use:
```php
try {
    $pdo = new PDO('mysql:dbname=test;host=localhost', 'username', 'password');
    // Execute queries
    unset($pdo);
} catch (PDOException $e) {
    echo $e->getMessage();
}
```

#### EXECUTING QUERIES
For simple queries that do not return results (INSERT, UPDATE, and DELETE) use exec() method:
```php
$q = 'DELETE FROM tablename';
$pdo->exec($q);
```
The ```exec()``` will return the number of rows affected by the query. False is returned if there is an error.

To get dynamically generated primary key after INSERT query:
```php
$id = $pdo->lastInsertId();
```
To prevent MySQL injections use quote() method:
```php
$data = $pdo->quote($unsafe_data);
$pdo->exec("INSERT INTO tablename (column) VALUES ($data)");
```
To execute queries that return results use query() method:
```php
$results = $pdo->query($q);
```
To fetch results directly use the loop or use fetch() method described below:
```php
foreach ($pdo->query($q) as $row) {
    // Use $row
}
```
To see how many records were return:
```php
$results->rowCount();
```
```$results``` variable will be an object of type PDOStatement. Use fetch() method to get results and use one of the constants to provide info on how to fetch the results. The constants could be:
- PDO::FETCH_ASSOC for an associative array
- PDO::FETCH_NUM for a numerically indexed array
- PDO::FETCH_OBJ for a generic object
- PDO::FETCH_CLASS for a specific type of object

```php
$results = $pdo->query('SELECT id, username FROM users');
$results->setFetchMode(PDO::FETCH_NUM);
while ($row = $results->fetch()) {
    // Use $row[0] for the id.
    // Use $row[1] for the username.
}
```
Example:
```php
class User {
    private $id;
    private $username;
    public getUsername() {
        return $this->username;
    }
}
$results = $pdo->query('SELECT id, username FROM users');
$results->setFetchMode(PDO::FETCH_CLASS, 'User');
while ($row = $results->fetch()) {
    echo $row->getUsername();  //The $row will be a User object and can use
                                 User methods! 
}
```

#### PREPARED STATEMENTS
Prepared statements is just a different way to run database queries. With prepared statements, the query is sent as one step and the specific data is sent separately.  It provides better performance and easier security management.
To use prepared statements with PDO invoke a ```prepare()``` method:
```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE email=? AND pass=SHA1(?)');
```
This query returns a PDOStatement object, which can be used in subsequent steps.
Next, invoke the ```execute()``` method with an array of actual values:
```php
$stmt->execute(array('me@example.com', 'mypass'));
```
Supply values in the same order as they'll be used in the query.

Another way is to use placeholders instead of the question marks:
```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE email=:email AND pass=SHA1(:pass)');
```
Then, use the named placeholders as keys in the array passed to the ```execute()``` method:
```php
$stmt->execute(array(':email' => 'me@example.com', ':pass' => 'mypass'));
```

#### Use array for binding:
```php
/* Query for inserting the user's account information */
$sql = 'SELECT user_id, username, password, status
        FROM hsr_user
        WHERE username = :username
        AND password = :password
        LIMIT 1;';
/* Instead of binding the params with ->bindParam(), we're going to bind params using an array */
        $values = array(':username' => $username,
                        ':password' => $password);
/* Prepare the SQL query to be safe for executing in the database */
        $statement = $dbconn->prepare($sql);
/* Execute the query passing the query the array of values */
        $statement->execute($values);
```
#### Access error messages
```php
$error = $stmt->errorInfo();
if (isset($error[2])) {
  echo $error[2];
}
```
