## Data Definition Language (DDL)

Table names must begin with a letter, must be 1-30 characters, contain numbers, letters, underscore, $ and #, have no duplicate name of any object owned by the same user, must not be a reserved word. Quoted identifiers are case-sensitive. A table can contain maximum of 1000 columns.
```
CREATE TABLE
```
Creates a new table. 

Syntax: 
```
CREATE TABLE table_name ( 
  column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],  ...);
```
Example:
```
CREATE TABLE customers ( 
  customer_id number(10) NOT NULL,
  customer_name varchar2(50) NOT NULL,
  city varchar2(50) );
```
Example with several constraints:
```
CREATE TABLE employees ( employee_number number(10) NOT NULL,
  employee_name varchar2(50) NOT NULL,
  department_id number(10),
  salary number(6),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number),
  CONSTRAINT fk_departments
    FOREIGN KEY (department_id)
    REFERENCES departments(department_id) );
```

Creates a table by copying all columns from another table.
```
Syntax:
CREATE TABLE new_table
  AS (SELECT * FROM old_table);
```
Example:
```
CREATE TABLE suppliers AS 
  (SELECT * FROM companies WHERE company_id < 5000);
```

Creates a table by copying selected columns from multiple tables.

Syntax:
```
CREATE TABLE new_table
  AS (SELECT column_1, column2, ... column_n
      FROM old_table_1, old_table_2, ... old_table_n);
```
Example:
```
CREATE TABLE suppliers
  AS (SELECT companies.company_id, companies.address, categories.category_type
      FROM companies, categories
      WHERE companies.company_id = categories.category_id
      AND companies.company_id < 5000);
```
Provide alias if the name of a column is an expression!

Example:
```
CREATE TABLE dept80 (account_profit) AS
	(SELECT retail - cost  FROM employees WHERE department Id = 80);
```
Creates a table from another table without copying any values from the old table.

Syntax:
```
CREATE TABLE new_table
  AS (SELECT * FROM old_table WHERE 1=2);
```
Example:
```
CREATE TABLE suppliers
  AS (SELECT * FROM companies WHERE 1=2);
```

#### DEFAULT
Used to input a default data if user does not put anything at all. Verify defaults in USER_TAB_COLUMNS table.

Example:
```
CREATE TABLE acctmanager (
  amid CHAR(4), amdate DATE DEFAULT SYSDATE, amcomm NUMBER (7,2) DEFAULT 0);
```

#### VIRTUAL COLUMN
Column defined by an expression that generates a value based on other column names in the table. Use AS keyword.

Example:
```
CREATE TABLE virtual (
  col1 NUMBER(2), col2(Number2), virt_col AS (col1 + col2));
```

#### DATA TYPES
- VARCHAR2(size) Variable-length character data (a maximum size must be specified, From 1 – 4000).
- CHAR[(size)] Fixed-length character data of size length (from 1 – 2000).
- NUMBER[(p,s)] Number having precision ( total number of decimal digits from 1 - 38 ) and scale (number of digits to   the right of the decimal point from -84 to 127). 
- DATE Date and time from Jan 1, 4712BC and Dec 31, 9999 AD.
- * TIMESTAMP store time as a date with fractional  seconds. y,m,d,h,m,s.
- ** WITH TIMEZONE
- ** WITH LOCALTIMEZONE
- * INTERVAL YEAR TO MONTH store time as an interval of years and months
- * INTERVAL DAY TO SECOND store time as an interval of d,h,min,sec (to represent precise difference)
- LONG Variable-length character data up to 2GB. (Can be used once per table, not copied when table is created using subqueries, cannot be included in GROUP BY or ORDER BY clause, no constraints can be defined) Better use CLOB!
- CLOB Character data up to 4GB.
- RAW(size) Raw binary data of maximum size length, but no more than 2000.
- LONG RAW Variable-length raw data up to 2GB.
- BLOB Binary data up to 4GB
- BFILE Binary data stored in an external file (up to 4GB)
- ROWID A base-64 number system to represent unique address of a row in its table.	

#### ALTER TABLE
Modifies table structure.

Syntax:
```
ALTER TABLE tablename ADD | MODIFY | DROP COLUMN | columnname [definition];
```
Adds a new column to the end (right side) of the table. The new column will be empty for all rows.

Example:
```
ALTER TABLE publisher ADD (ext NUMBER(4));
```
Changes an existing column’s definition such as size, datatype, defaults, use MODIFY clause. A new column must be as wide as the data fields it already contains. It is impossible to decrease NUMBER datatype if data already exists. Changing default value does not change data already present in the table. Possible to modify many columns at once.

Example:
```
ALTER TABLE acctmanager MODIFY (amlast VARCHAR2(18));
```
Deletes an existing column. Can reference to only one column. Deletion is permanent!  Cannot delete the last remaining column in the table. A primary key cannot be dropped from the table.

Example:
```
ALTER TABLE publisher DROP COLUMN ext;
```
Use SET UNUSED clause to mark the column for deletion at a later time. The column will not be available and not displayed in the table structure. Data will be lost. Use DROP UNUSED to completely remove the column. Only one column may be altered at a time. If you have lots of data use SET UNUSED instead  DROP COLUMN.

Examples:
```
ALTER TABLE tablename SET UNUSED (columnname);
ALTER TABLE tablename SET UNUSED COLUMN columnnam;
ALTER TABLE tablename DROP UNUSED COLUMNS;
```
Changes table structure or put a table into read-only mode to prevent DDL or DML changes during table maintenance. Possible to drop the table!

Example:
```
ALTER TABLE employees READ ONLY;
ALTER TABLE employees READ WRITE;
```
Rrenames a table or column.

Example:
```
ALTER TABLE customers RENAME TO contacts;
```
Example:
```
ALTER TABLE tablename RENAME COLUMN columnname TO newcolumnname;
```

#### TRUNCATE TABLE
Deletes all data from the table right away leaving the table structure intact. Only possible if referential integrity constraint allows. It frees up storage space!

Example:
```
TRUNCATE TABLE tableneame;
```

#### DROP TABLE 
Moves a table to the recycling bin or removes all data entirely. Views and synonyms remain, but invalid, pending transactions committed. Use FLASHBACK TABLE statement to restore a dropped table from recycling bin.

Example:
```
DROP TABLE tablename [PURGE]; 
```
Use PURGE keyword to drop the table completely and free up space, bypassing recycle bin.

#### FLASHBACK
Restores objects from the recycle bin.

Example:
```
FLASHBACK TABLE tablename TO BEFORE DROP;
```
To clear recyclebin use PURGE RECYCLEBIN;

#### CONSTRAINTS
Use with CREATE TABLE or ALTER TABLE commands. Oracle adds constraint names implicitly. However, better to add the constraints explicitly. Add keyword CONSTRAINT with a constraint name in format:
```
tablename_columnname_constrainttype. 
```
Constraint types: Primary Key - _pk, Foreign Key - _fk, Unique - _uk, Check - _ck, Not Null - _nn.

Get info on all constraints in USER_CONSTRAINTS or USER_CONS_COLUMNS system dictionary tables.

#### NOT NULL 
NOT NULL means that the column cannot contain a null value (must defined at the column-level). When adding constraint to an existing table, use ALTER TABLE … MODIFY. Do not use with DEFAULT!

Examples:
```
ALTER TABLE orders MODIFY (customer# CONSTRAINT orders_customer#_nn NOT NULL); 
ALTER TABLE orders MODIFY (customer# NOT NULL);
```
#### UNIQUE
UNIQUE means values must be unique for all rows in the table. Allows NULL values!

Example:
```
ALTER TABLE books ADD CONSTRAINT books_title_uk UNIQUE (title);
```

#### PRIMARY KEY 
Uniquely identifies each row of the table. Does not allow NULL values! No need to put UNIQUE!

Examples:
```
ALTER TABLE customers 
  ADD CONSTRAINT customers_customer#_pk PRIMARY KEY (customer#);
ALTER TABLE orderitems 
  ADD CONSTRAINT orderitems_pk PRIMARY KEY (order#, item#);
```
#### FOREIGN KEY 
Enforces referential integrity. Must match an existing value in the parent table or be NULL. Default is a restrict rule, which disallows the update or deletion of referenced data.

Examples:
```
ALTER TABLE orders 
  ADD CONSTRAINT orders_customer#_fk FOREIGN KEY (customer#) 
      REFERENCES customers (customer#); 
CREATE TABLE emp (id NUMBER(7), last_name VARCHAR2(25), dept_id NUMBER(7) 
 CONSTRAINT emp_dept_id_fk REFERENCES dept (id));
```
- REFERENCES keyword identifies the table and column in the parent table.
- ON DELETE CASCADE deletes the dependent rows in the child table when a row in the parent is deleted. 
- ON DELETE SET NULL converts dependent foreign key valued to null. Used by default.

Example:
```
ALTER TABLE orders 
  ADD CONSTRAINT orders_custromer#_fk FOREIGN KEY (customer#) 
      REFERENCES customers (customer#) ON DELETE CASCADE;
```
To delete a parent table with foreign key in child table drop the child table first and then drop the parent table or drop the parent table with the CASCADE CONSTRAINS option:
```
DROP TABLE customers CASCADE CONSTRAINTS;	
```
#### CHECK
Specifies a condition that must be true. A single value can have multiple CHECK values:
```
ALTER TABLE orders 
  ADD CONSTRAINT orders_shipdate_ck CHECK (orderdate <= shipdate);
```
Table-level constraints (preferable), where constraint is separate from column definition. List the constraint after all columns are defined.

Example:
```
CREATE TABLE dept (deptid NUMBER(2), dname VARCHAR2(20) NOT NULL, fax VARCHAR2(12),
 CONSTRAINT dept_deptid_pk PRIMARY KEY (deptid),
 CONSTRAINT dept_dname_uk UNIQUE (dname));
```
**Column-level constraints**. The constraint is a part of column definition. If the constraint is applied more than one column (composite key) use table-level constraint.

Example:
```
CREATE TABLE dept (deptid NUMBER(2) CONSTRAINT dept_deptid_pk PRIMARY KEY,
 dname VARCHAR2(20) NOT NULL CONSTRAINT dept_dname_uk UNIQUE,
 fax VARCHAR2(12));
```
Constraints with no names assigned:
```
CREATE TABLE dept (deptid NUMBER(2) PRIMARY KEY, 
  dname VARCHAR2(20) NOT NULL  UNIQUE, fax VARCHAR2(12));
```
To disable constraints while inserting large amount of data use DISABLE keyword:
```
ALTER TABLE equip DISABLE CONSTRAINT equip_rating_ck;
ALTER TABLE equip ENABLE CONSTRAINT equip_rating_ck;
```
To remove constraint use DROP keyword:
```
ALTER TABLE equip DROP CONSTRAINT equip_rating_ck;
ALTER TABLE equip DROP PRIMARY KEY CASCADE;  (drops a primary key referenced by a foreign key)
```
To drop all constraints for columns: 
```
ALTER TABLE equip DROP COLUMN emp_id CASCADE CONSTRAINTS;
```
To see all constraints on all of the tables in your database:
```
SELECT * FROM USER_CONSTRAINTS;
```
To see all constraints on specific tables:
```
SELECT * FROM USER_CONSTRAINTS WHERE table_name IN (‘PETS’, ‘SPECIES’);
```

#### EXTERNAL TABLES
An external table is a read-only table which metadata is stored in the database but whose data is stored outside the database. No DML is possible on the external tables, but it is possible to upload data to a new internal table from the external table using CREATE TABLE AS SELECT …
- ORACLE_LOADER driver is used for reading data from external files.
- ORACLE_DATAPUMP driver is used to import and export data using a platform-independent format. 

To create an external table first create a directory (must have CREATE ANY DIRECTORY system privilege):
```
CREATE OR REPLACE DIRECTORY emp_dir AS ‘/…/emp_dir’;
GRANT READ ON DIRECTORY emp_dir TO hr;
```

Then create a table:
```
CREATE TABLE old_emp (fname CHAR(25), lname CHAR(25)) 
ORGANIZATION EXTERNAL (TYPE ORACLE_LOADER DEFAUL DIRECTORY emp_dir 
  ACCESS PARAMETERS (RECORDS DELIMITED BY NEWLINE NOBADFILE NOLOGFILE FIELDS
    TERMINATED BY ‘,’ (fname POSITION (1:20) CHAR, lname POSITION (22:41)  
    CHAR)) LOCATION (‘emp.dat’))
PARALLEL 5 REJECT LIMIT 200;
```
If all successful, the old_emp external table can be queried like a normal table: 
```
SELECT * FROM old_emp;
```

#### COMMENTS
Adds comments to a table.

Example:
```
COMMENT ON TABLE furniture IS 'This furniture table created mm/dd/yyyy by 
    your name here as part of the 152-125 course'; 
```
Maximum length of comment is 4000 characters.

To see the comments:
```
SELECT * FROM USER_TAB_COMMENTS;
```
To add comments to an individual column:
```
COMMENT ON COLUMN furniture.cost IS 'Cost is the total cost to me 
    to acquire this piece of furniture, including transportation cost';
```
To see the comments: 
```
SELECT  * FROM USER_COL_COMMENTS;
```

To see information about all custom database objects:
```
SELECT * FROM USER_OBJECTS;
```
To see information about all tables the user have use USER_TABLES view.
To see all tables the user can access use ALL_TABLES view.
