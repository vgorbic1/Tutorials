## Create, Read, Update, and Delete Operations
Login to the MySQL shell as a root or priveleged user.

Select a database.

### Create
To add data to a table use this example:
```sql
INSERT INTO potluck (id, name, food, confirmed, signup_date) 
  VALUES (NULL, "John", "Casserole","Y", '2012-04-11');
```
To add a new column to the table (after a specific column):
```sql
ALTER TABLE potluck ADD email VARCHAR(255) AFTER name;
```

### Read
To take a look at the table after adding data:
```sql
SELECT * FROM potluck
```

### Update
To update data at a table use this example:
```sql
UPDATE potluck SET confirmed = 'Y' WHERE potluck.name = 'Sandy';
```

### Delete
To delete data from a table field use this example:
```sql
UPDATE potluck SET confirmed = 'null' WHERE potluck.name = 'Sandy';
```
To delete a column use this example:
```sql
ALTER TABLE potluck DROP email;
```
To delete a row use this template:
```sql
DELETE from [tablename] where [columnname]=[field];
```
To remove all data from the table, but leave the structure intact:
```sql
TRUNCATE TABLE tablename
```
If you are using InnoDB tables, MySQL will check if there are any foreign key constraints available in the tables 
before deleting data. The following are cases:
- If the table has any foreign key constraints, the `TRUNCATE TABLE` statement deletes rows one by one. If the foreign key 
constraint has `DELETE CASCADE` action, the corresponding rows in the child tables are also deleted.
- If the foreign key constraint does not specify the `DELETE CASCADE` action, the `TRUNCATE TABLE` deletes rows one by one, 
and it will stop and issue an error when it encounters a row that is referenced by a row in a child table.
- If the table does not have any foreign key constraint, the `TRUNCATE TABLE` statement drops the table and recreates a 
new empty one with the same structure, which is faster and more efficient than using the `DELETE` statement especially 
for big tables.
- If you are using other storage engines, the `TRUNCATE TABLE` statement just drops and recreates a new table.

Notice that the `TRUNCATE TABLE` statement resets auto increment value to zero if the table has an `AUTO_INCREMENT` column.
