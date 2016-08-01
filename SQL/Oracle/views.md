## VIEWS
Views are database objects that store a SELECT statement and allow using a query’s results as a table. They simplify issuing complex SQL queries and restrict user’s access to sensitive data.
- Simple view is based on a subquery that references only one table and does not include group functions, expressions, or GROUP BY clauses.
- Complex view is based on a subquery that references or derives data from one or more tables and can contain functions or grouped data.
- Materialized view replicates data by physically storing the view query’s results.

#### CREATE VIEW
Used to create views.

Syntax:
```
CREATE [OR REPLACE] [FORCE | NOFORCE] VIEW viewname (columnname, …) 
  AS subquery 
 [WITH CHECK OPTION [CONSTRAINT constraintname] (prevents from updates enforced in WHERE clause) 
 [WITH READ ONLY]; (prevents performing any DML commands and constraints above are not needed)
``` 
NOFORCE is default and indicates that all tables must be valid, otherwise FORCE may create views based on tables that are not exist yet.

Columname – use if you want to assign new names to the columns in the view, or use column aliases directly in the query. 

You cannot have ORDER BY clause in subquery!

Example:
```
CREATE VIEW sup_orders AS
  SELECT suppliers.supplier_id, orders.quantity, orders.price
  FROM suppliers
  INNER JOIN orders
  ON suppliers.supplier_id = orders.supplier_id
  WHERE suppliers.supplier_name = 'Microsoft';
```

#### DML on VIEWS
As long as the view isn’t created with the WITH READ ONLY option, any DML operation is allowed if it doesn’t violate an existing constraint on the underlying table. In complex views columns that derived from a function or an expression should have names listed immediately after keyword VIEW or should have aliases in SELECT clause.
For complex views DML restrictions exist:

You can add data to the view unless:
-	There are Group functions exist
-	A GORUP BY clause present
-	DISTINCT (UNIQUE) keyword present
-	Pseudocolumn POWNUM keyword present

You can modify the view unless:
-	There are Group functions exist
-	A GORUP BY clause present
-	DISTINCT (UNIQUE) keyword present
-	Pseudocolumn POWNUM keyword present
-	Columns defined by expressions (for example, SALARY*12)
-	Columns defined by expressions (for example, SALARY*12)
-	There are NOT NULL columns in the base tables that are not selected by the view

You can remove a row unless:
-	There are Group functions exist
-	A GORUP BY clause present
-	DISTINCT (UNIQUE) keyword present
-	Pseudocolumn POWNUM keyword present

#### DROP VIEW
When view is dropped, data is not deleted. Only the creator or a user with the DROP ANY VIEW privilege can remove a view.

Syntax:
```
DROP VIEW viewname; 
```

#### INLINE VIEW
Inline view is a subquery used in the FROM clause of a SELECT statement to create a “temporary” table that can be referenced by the outer query’s SELECT and WHERE clauses.

Syntax:
```
SELECT columnname, … FROM (subquery) WHERE ROWNUM <= N;
```
Example on how to get five most profitable books:
```
SELECT title, profit
FROM (SELECT title, retail-cost profit FROM books ORDER BY retail-cost DESC) WHERE ROWNUM <=5;
```
To see all information about user created views use USER_VIEWS.

