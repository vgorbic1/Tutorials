## INDEXES
An index is a performance-tuning method of allowing faster retrieval of records. By default, Oracle creates B-tree (balanced-tree) indexes. The indexes created automatically on primary keys and unique constraints.

#### CREATE INDEX
Creates an index. Create an index when:
-	A column contains a wide range of values
-	A column contains a large number of NULL values
-	One or more columns are frequently used together in a WHERE clause or a join condition
-	The table is large and queries retrieves only up to 4% of the rows in the table

Syntax:
```
CREATE [UNIQUE] INDEX index_name
  ON table_name (column1, column2, ... column_n)
  [ COMPUTE STATISTICS ];
```  
Example:
```
CREATE INDEX supplier_idx
  ON supplier (supplier_name);
```

#### FUNCTION BASED INDEXES
In Oracle, you are not restricted to creating indexes on only columns. You can create function-based indexes.

Syntax:
```
CREATE [UNIQUE] INDEX index_name
  ON table_name (function1, function2, ... function_n)
  [ COMPUTE STATISTICS ];
```

Example:
```
CREATE INDEX supplier_idx
  ON supplier (UPPER(supplier_name));
```
Indexes can be performed on multiple tables. Maximum number of columns in B-tree index is 32.
Heap-organized table – unordered collection of data, so in full-scan all table should be red in order to find a certain record (very slow with huge tables).
Bitmap index is useful for improving queries on columns that have low selectivity.

To create Index with a new table explicitly use it with CREATE TABLE statement.

Example:
```
CREATE TABLE emp2 (employee_id NUMBER(6) PRIMARY KEY USING INDEX (CREATE INDEX emp_id ON emp2(employee_id)), first_name VARCHAR2(20);
```

#### ALTER INDEX
You cannot modify index! Only rename it! 

Example:
```
ALTER INDEX customers_idx RENAME TO books_idx;
```

#### DROP INDEX
Removes index. Indexes dropped automatically when a table is dropped.

Example:
```
DROP INDEX supplier_idx;
```
Check for indexes in the USER_INDEXES view or in the USER_IND_COLUMNS view.
