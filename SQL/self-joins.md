##Self Joins
The SQL SELF JOIN is used to join a table to itself as if the table were two tables, temporarily renaming at least one table in the SQL statement.
```sql
SELECT a.column_name, b.column_name...
FROM table1 a, table1 b
WHERE a.common_field = b.common_field;
```
![self-join-example](https://cloud.githubusercontent.com/assets/13823751/18753532/4139b0d4-80ab-11e6-97a2-dbff95e35317.jpg)
