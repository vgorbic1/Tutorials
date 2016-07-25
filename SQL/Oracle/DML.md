##DML

####INSERT
Inserts new rows of data to a table. Use single quotes for nonnumeric data. The order of columns is not important, as long as the columns match their values. When inserting records into a table using the INSERT statement, you must provide a value for every NOT NULL column. You can omit a column from the Oracle INSERT statement if the column allows NULL values.

Syntax:
```
INSERT INTO tablename [(columnname, …)]
VALUES (datavalue, …);
```
To insert a blank value (NULL) do not include the coulumname in the list or use two single quotes ‘’ as a value or use NULL keyword as a value.

Example:
```
INSERT INTO suppliers (supplier_id, supplier_name)
VALUES (5000, 'Apple');
```
#### SYSDATE: 
Insert a column list in the INSERT INTO clause that omits the date column or use the keyword DEFAULT for the column value. 

To treat a single quote as part of a string value, enter two single quotes together in the value:
```
VALUE (‘One’, ‘user’’s’)
```
To insert data from an existing table:
```
INSERT INTO acctbonus (amid, amsal, region)
  SELECT amid, amsal, region FROM acctmanager; (do not use VALUES clause!)
```
To insert multiple rows (may be used as a pivoting insert if you specify a table and columns in select statement):
```
INSERT ALL
  INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM')
  INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft')
  INTO suppliers (supplier_id, supplier_name) VALUES (3000, 'Google')
SELECT * FROM dual;
```
Conditional insert with ALL:
```
INSERT ALL
  WHEN hiredate < ’01-JAN-95’ THEN
   INTO emp_history VALUES (emp_id, hiredate, sal)
  WHEN comm IS NOT NULL THEN
   INTO emp_sales VALUES(emp_id, comm, sal)
   SELECT employee_id AS emp_id, hiredate, salary AS sal, commission AS comm
   FROM employees;
```
Conditional insert with FIRST

For each employee record, it is inserted into the very first target table that meets the condition.
```
INSERT FIRST
WHEN salary < 5000 THEN
 INTO sal_low VALUES (employee_id, last_name, salary)
WHEN salary BETWEEN 5000 AND 10000 THEN
 INTO sal_mid VALUES (employee_id, last_name, salary)
ELSE
INTO sal_high VALUES (employee_id, last_name, salary)
SELECT employee_id, last_name, salary FROM employees;
```
To insert data using a subquery:
```
INSERT INTO (SELECT location_id, city, country
             FROM location WHERE region = 'Europe'
  WITH CHECK OPTION) <–this prohibits from changing rows that are not in the subquery
VALUES (3300, 'Cardiff', 'UK');
```

#### UPDATE
Changes the contents of existing rows. Preferably, use primary key in WHERE clause. There are 2 syntaxes for an update query in Oracle depending on whether you are performing a traditional update or updating one table with data from another table.

Syntax for the UPDATE statement when updating one table:
```
UPDATE table
SET column1 = expression1, column2 = expression2, ... 
WHERE conditions;
```
Syntax for the UPDATE statement when updating one table with data from another table:
```
UPDATE table1
SET column1 = (SELECT expression1 FROM table2 WHERE conditions),
    Column2 = (SELECT expression2 FROM table2 WHERE conditions),
WHERE conditions;
```
Example 1:
```
UPDATE customers
SET state = 'California',
    customer_rep = 32
WHERE customer_id > 100;
```
Example 2:
```
UPDATE employees
SET job_id = (SELECT job_id FROM employees WHERE employee_id = 205),
       salary = (SELECT salary FROM employees WHERE employee-id = 205)
WHERE employee_id = 113;
```
Example 3:
```
UPDATE employees
SET manager_id = DEFAULT (if there is a default value for this column)
WHERE employee_id = 113;
```
#### Correlated UPDATE
Use a correlated subquery to update rows in one table based on rows from another table:
```
UPDATE table1 alias1
SET column = (SELECT expression
FROM table2 alias2
WHERE alias1.column = alias2.column);
```

#### DELETE
Deletes date from specific rows. DELETE applies to the entire row, not a specific column!

Syntax:
```
DELETE FROM table
WHERE conditions;
```
Example:
```
DELETE FROM customers
WHERE last_name = 'Smith';
```
#### Correlated DELETE

Use a correlated subquery to delete rows in one table based on rows from another table.
```
DELETE FROM table1 alias1
WHERE column operator
     (SELECT expression
      FROM table2 alias2
      WHERE alias1.column = alias2.column);
```

#### TRUNCATE
Removes all records from a table in Oracle. It performs the same function as a DELETE statement without a WHERE clause. It can not be rolled back!

Example:
```
TRUNCATE TABLE customers;
```

#### MERGE
Conditionally inserts, updates or deletes rows in a table:
```
MERGE INTO copy_emp3 c
  USING (SELECT * FROM employees ) e
  ON (c.employee_id = e.employee_id)
    WHEN MATCHED THEN
  UPDATE SET
  c.first_name = e.first_name,
  c.last_name = e.last_name,
   ...
  DELETE WHERE (e.commission_pct IS NOT NULL)
    WHEN NOT MATCHED THEN
INSERT VALUES(e.employee_id, e.first_name, ...);
```

#### TRANSACTION CONTROL
Transaction control allows to save or undo changes. All DML statements stay in transaction queue until it saved or undone. Transaction occurs when one or several DML statements were issued and not committed. 
When DDL commands are issued, Oracle, by default, performs a row-level block, so no one can change the row. In addition a lock is placed on the table, so no one can lock the whole table while the row lock is active. It is a shared lock, so users can view data stored in the table, but cannot modify it. Use LOCK TABLE command in share mode to explicitly lock the table:
- LOCK TABLE tablename IN SHARE MODE;
When DDL operations are performed, Oracle places an exclusive lock on the table so that no other user can alter the table. Now no one can place another exclusive or shred lock on that table:
- LOCK TABLE tablename IN EXCLUSIVE MODE;
Locks are released automatically if ROLLBACK or COMMIT is issued.
- FOR UPDATE command places a shared lock on the records to be changed and prevents any other user from acquiring a lock on the same records:
```
SELECT columnname FROM tablename [WHERE condition] FOR UPDATE;
```
Use COMMIT or ROLLBACK to release the lock. 

#### COMMIT / ROLLBACK / SAVEPOINT
COMMIT permanently saves the DML statements issued previously. It implicitly occurs when you exit client tools or if a DDL command is issued after DML statement.  
A DML statement may be undone by ROLLBACK transaction control command.
SAVEPOINT is like a bookmark in transaction. It allows to roll back to a specific point within the transaction.
Use SAVEPOINT savepoint and ROLLBACK TO savepoint syntax, where savepoint is any string to name the savepoint. If you created a second savepoint with the same name as an earlier savepoint, the earlier savepoint is deleted.

Tracking Changes in Data

#### VERSIONS BETWEEN
Retrieves all the versions of the rows that exist or have ever existed between the time the query was issued and a point back in time.
```
SELECT versions_starttime "START_DATE",versions_endtime "END_DATE", salary
FROM employees
VERSIONS BETWEEN SCN MINVALUE AND MAXVALUE
WHERE last_name = 'Lorentz';
```
