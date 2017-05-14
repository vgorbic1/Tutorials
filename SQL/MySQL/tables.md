## Managing Tables
Login to the MySQL shell as a root or a privileged user.

Select a database.

To show all tables in the database:
```sql
SHOW TABLES
```
To create a basic table use the following example:
```sql
CREATE TABLE potluck (
 id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
 name VARCHAR(255),
 food VARCHAR(255),
 confirmed CHAR(1), 
 signup_date DATE);
```
MySQL requires that `date` datatype be written as `yyyy-mm-dd`.
 
To see the table structure:
```sql
DESCRIBE tablename
```
To remove a table from the database:
```
DROP TABLE tablename;
```
