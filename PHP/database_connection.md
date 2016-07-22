## Database Connection with mysqli

#### Write to a database
Make a connection with the database:
```PHP
$dbc = mysqli_connect('website.com', 'username', 'password', 'database_name')
  or die('Error connecting to MySQL server.'); 
```
Create a SQL query string to pass to the database:
```PHP
$query = "INSERT INTO mytable (values, variables)
          VALUES('value', '$variable')";
```
Send the query to the database:
```PHP
$result = mysqli_query($dbc, $query)
  or die('Error querying database.');
```
Close connection:
```PHP
mysqli_close($dbc);
```

#### Read from a database
Make a connection with the database:
```PHP
$dbc = mysqli_connect('website.com', 'username', 'password', 'database_name')
  or die('Error connecting to MySQL server.'); 
```
Create a SQL query string to pass to the database:
```PHP
$query = "SELECT * FROM mytable";
```
Send the query to the database:
```PHP
$result = mysqli_query($dbc, $query)
  or die('Error querying database.');
```
the `$result` stores an ID number for MySQL resource. To actually see the data that resource ID has use `mysqli_fetch_array()`

Get one row from the query results:
```PHP
$row = mysqli_fetch_array($result);
```
Display one row content:
```PHP
$row['first_column_name'];
$row['second_column_name'];
```
To display the whole table of query results use WHILE loop:
```PHP
while($row = mysqli_fetch_array($result)) {
    echo $row['first_name'];
    echo $row['second_name'];
}
```
Close connection:
```PHP
mysqli_close($dbc);
```
