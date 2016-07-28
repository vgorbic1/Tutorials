## SEQUENCES
A sequence a.k.a. AUTONUMBERS generates sequential integers that can be used to assist with internal controls or serve as primary keys for tables. One sequence can be used with any tables or views within the database.

#### CREATE SEQUENCE
Creates a sequence.

Syntax:
```
CREATE SEQUENCE sequencname 
  [INCREMENT BY value] (this is an interval. Can be negative, but use START WITH and both MAXVALUE and MINVALUE) 
  [START WITH value] (use when import existing data)
  [MAXVALUE value] (establishes max value for the sequence. Can be NOMAXVALUE as it is by default)
  [MINVALUE value] 
  [CYCLE] (should we reuse values after reaching the end of sequence? NOCYCLE is default)
  [ORDER] (the order of returning values. NOORDER is default)
  [CACHE value]; (generates a set of values ahead, to speed up process. CACHE 20 is default. Can be NOCACHE)
```
Example 1:
```
CREATE SEQUENCE customers_seq;
```
Example 2:
```
CREATE SEQUENCE supplier_seq
  MINVALUE 1
  MAXVALUE 999999999999999999999999999
  START WITH 1
  INCREMENT BY 1
  CACHE 20;
```
Use pseudocolumn NEXTVAL to generate the next sequence value:
```
Customers_seq.NEXTVAL;
```
Example:
```
INSERT INTO suppliers (supplier_id, supplier_name)
VALUES (supplier_seq.NEXTVAL, 'Kraft Foods');
```
Use pseudocolumn CURRVAL to view the current sequence value:
```
Customers_seq.CURRVAL;
```

#### ALTER SEQUENCE
Used to change the sequence, but it will alter only new values. START WITH cannot be changed.

Example:
```
ALTER SEQUENCE seq_name
INCREMENT BY 124;
```

#### DROP SEQENCE
Used to drop a sequence.

Example:
```
DROP SEQUENCE supplier_seq;
```
You cannot use NEXTVAL or CURRVAL in context of:
-	SELECT list of a view
-	SELECT with DISTINCT or GROUP BY, HAVING, ORDER BY clauses
-	A subquery in a SELECT, DELETE, or UPDATE statement
-	DEFAULT expression in a CREATE TABLE ir ALTER TABLE

Gaps in sequence values can occur when:
-	Rollback occurs
-	System crashes
-	A sequence is used in another table

Find all sequences created by the user in USER_SEQUENCES table.
