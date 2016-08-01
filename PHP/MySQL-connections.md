## My SQL connection
#### With original MySQL extension:
| --- | --- | --- |
| Connect | $conn = mysql_connect($h, $u, $p); | Need hostname, username and password |
| Coose DB | mysql_select_db('dbName'); | Server connection can be second, optional argument |
| Submit query | $result =  mysql_query($sql); | Requires a query, server connection may be second optional argument |
| Count results | $numRows = mysql_num_rows($result); | Takes result set as sole argument |
| Extract record | $row = mysql_fetch_assoc($result); | Takes result as a sole argument. Extracts current record as an associative array |
| Extract record | $row = mysql_fetch_row($result); | Takes result as a sole argument. Extracts current record as indexed array.

#### With MySQL Improved object-oriented interface:
