## My SQL connection
#### With original MySQL extension:
| Action | Usage | Comments |
| --- | --- | --- |
| Connect | $conn = mysql_connect($h, $u, $p); | Needs hostname, username and password. |
| Choose DB | mysql_select_db('dbName'); | Server connection can be second, optional argument. |
| Submit query | $result =  mysql_query($sql); | Requires a query, server connection may be second optional argument. |
| Count results | $numRows = mysql_num_rows($result); | Takes result set as sole argument. |
| Extract record | $row = mysql_fetch_assoc($result); | Takes result as a sole argument. Extracts current record as an associative array. |
| Extract record | $row = mysql_fetch_row($result); | Takes result as a sole argument. Extracts current record as an indexed array. |

#### With MySQL Improved object-oriented interface:
| Action | Usage | Comments |
| --- | --- | --- |
| Connect | $conn = new mysqli($h, $u, $p, $d); | Needs hostname, username, password and database name. |
| Choose DB | $conn->select_db('dbName'); | Use to select different database. |
| Submit query | $result =  $conn->query($sql); | Returns result object. |
| Count results | $numRows = $result->num_rows; | Return number of rows in result object. |
| Release DB resources | $result->free_result(); | Frees up connection to allow new query. |
| Extract record | $row = $result->fetch_assoc(); | Extracts current record from result object as an associative array. |
| Extract record | $row = $result->fetch_row(); | Extracts current record from result object as an indexed array. |

#### With MySQL PDO interface:
| Action | Usage | Comments |
| --- | --- | --- |
| Connect | $conn = new PDO(DSN, $u, $p); | Needs data source name (DSN) username and password. Must be wrapped in try/catch block. |
| Choose DB |  | You are doing that in DSN above |
| Submit query | $result =  $conn->query($sql); | Returns result object. Can also be used inside forech loop to extract each record. |
| Count results | | Use SELECT COUNT(*) in SQL query. |
| Get single result | $item = $result->fetchColumn() | Gets first record in first column of result. To get result from other columns, use column number (from 0) as argument. |
| Get next record | $row = $result->fetch(); | Gets next row from result set as associative array. |
| Release DB resources | $result->closeCursor(); | Frees up connection to allow new query. |
| Extract records | foreach($conn->query($sql) as $row) { | Extracts current row from result set as associative array. |
When using PDO with MySQL, the data source name (DSN) is a string that takes the following format:
```
'mysql:host=yourhostname;dbname=yourdatabasename'
```
or with a port number, if it is nonstandard:
```
'mysql:host=yourhostname;port=3307;dbname=yourdatabasename'
```
