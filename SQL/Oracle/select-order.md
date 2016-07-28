## SELECT
Used to retrieve records from one or more tables in an Oracle database.

Syntax:
```
SELECT [DISTINCT | UNIQUE] (*, columname [AS alias, …)
FROM tablename
[WHERE condition]
[GROUP BY group_by_expression]
[HAVING group_condition]
[ORDER BY columnname]
```
- WHERE clause specifies conditions that must be true for a record to be included in query results.
- ORDER BY specifies the sorted order for displaying query results.

Table alias can be no longer than 30 characters.

Comparison operators: =, <, >, <=, >=, <>, !=, ^=, BETWEEN … AND, IN, LIKE, IS NULL

Logical operators: AND, OR, NOT

#### Rules of Precedence:
1.	Arithmetic operators
2.	Concatenation operators
3.	Comparison operators
4.	IS [NOT] NULL, LIKE, [NOT] IN
5.	[NOT] BETWEEN
6.	Not equal to
7.	NOT logical condition
8.	AND logical condition
9. OR logical condition

To select an empty column (no data in rows) use SELECT ‘ ‘ 

#### WHERE
WHERE keyword is responsible for selection process. No aliases allowed within the WHERE clause.

Example 1:
```
SELECT * FROM address
WHERE state = ‘FL’; (string literal – use single quotes)
Example 2:
SELECT * FROM address
WHERE customer# = 1010; (no single quotes, but will still work with quotes. It depends on what the field defined to hold: a numerical data or char data. Check with DESC)
Example 3:
SELECT * FROM address
WHERE pubdate = ’21-JAN-05’ (must be enclosed in single quotes)
```

#### COMPARISON OPERATORS
Used with numbers, text, and date fields.

Examples:
```
WHERE retail > 55
WHERE title >= ‘HO’ (string literal – use single quotes)
WHERE orderdate < ‘01-APR-09’ ( < means dates before ) ( > means dates after )
WHERE pubid [NOT] BETWEEN 1 AND 3; (Inclusive operator! Means >= and <= )
WHERE orderdate [NOT] BETWEEN ’01-APR-09’ AND ’04-APR-09’ (Inclusive operator! Means >= and <= )
WHERE title [NOT] BETWEEN ‘A’ AND ‘D’ (Not inclusive !!! ‘D’ is not included. String literal – use single quotes)
WHERE publid [NOT] IN (1,2,3) (matching one of the values listed. Like many OR operators)
WHERE state [NOT] IN (‘CA’,’TX’) (string literal – use single quotes)
```

#### LIKE 
Like is used with wildcard characters to search for patterns.

Wildcard characters: % any number of characters (zero, one, or more),  _ exactly one character.

Example:
```
SELECT * FROM address
WHERE lastname LIKE ‘P%’; (string literal – use single quotes) Starts with capital P and has any number of chars after.
ESCAPE option is used when literal % and _ needed:
```
Examples:
```
SELECT * FROM address
WHERE tvalue LIKE’\%_A%T’ ESCAPE ‘\’; (means use \ as an Escape character for any chars within the pattern)
SELECT * FROM address
WHERE tvalue LIKE’*%-A%T’ ESCAPE ‘*’ (any chars may be used as an escape character) 
```

#### LOGICAL OPERATORS
```
AND (both conditions must evaluate as TRUE)
```

Example:
```
SELECT * FROM address
WHERE pubid = 3 AND category = 'COMPUTER'
OR (one of the conditions must evaluate as TRUE)
```
Example:
```
SELECT * FROM address
WHERE pubid = 3 OR category = 'COMPUTER';
```
Use IN operator to specify many ORs.

#### IS NULL
It means that no value has been stored in this field.
Cannot use = because there is nothing to compare with. You are checking for the status of the column.

Examples:
```
SELECT * FROM address
WHERE shipdate IS NULL; (looks for all values in the column that are of NULL type)
SELECT * FROM address
WHERE shipdate IS NOT NULL; (looks for any values that are not of NULL type)
```

#### ORDER BY
Display results in a sorted order: ascending or descending.

The ASC (default) order of sorting:
-	Blank and special characters
-	Numeric values
-	Character Values (uppercase first)
-	NULL values

Examples:
```
SELECT * FROM address
ORDER BY name DESC; (To reverse the order use DESC)

SELECT * FROM address
ORDER BY “All Names”; (alias as a column name may be used)

SELECT * FROM address
ORDER BY referred NULLS FIRST (changes the order of showing NULL values in ascending)

SELECT * FROM address
ORDER BY referred DESC NULLS LAST (changes the order of showing NULL values in descending)
```

#### SECONDARY SORT
The limit on column numbers is 255.

Example:
```
SELECT * FROM address
ORDER BY state DESC, city; 
```
sort first by state in descending order and then by city in ascending order.

When SELECT DISTINCT or UNIQUE is used, ORDER BY must have columns listed for sorting.
Use the number of columns in SELECT clause to produce multiple sorting.

Example:
```
SELECT lastname, firstname, state, city
FROM customers
WHERE state IN(‘FL’,’CA’)
ORDER BY 3 DESC, 4;
```
If all successful, the old_emp external table can be queried like a relational table: SELECT * FROM old_emp;

#### Hierarchical Queries
If a table contains hierarchical data, then you can select rows in a hierarchical order using the hierarchical query clause. To find the children of a parent row, Oracle evaluates the PRIOR expression of the CONNECT BY condition for the parent row and the other expression for each row in the table. Rows for which the condition is true are the children of the parent. The CONNECT BY condition can contain other conditions to further filter the rows selected by the query. The CONNECT BY condition cannot contain a subquery.

Example 1: the following hierarchical query uses the CONNECT BY clause to define the relationship between employees and managers:
```
SELECT employee_id, last_name, manager_id
   FROM employees
   CONNECT BY PRIOR employee_id = manager_id;
```
Example 2: START WITH clause to specify a root row for the hierarchy and an ORDER BY clause using the SIBLINGS keyword to preserve ordering within the hierarchy:
```
SELECT last_name, employee_id, manager_id, LEVEL
      FROM employees
      START WITH employee_id = 100
      CONNECT BY PRIOR employee_id = manager_id
      ORDER SIBLINGS BY last_name;
```
Example 3: Formatting Hierarchical Reports Using LEVEL and LPAD. Create a report displaying company management levels, beginning with the highest level and indenting each of the following levels.
```
COLUMN org_chart FORMAT A12
SELECT LPAD(last_name, LENGTH(last_name)+(LEVEL*2)-2,'_')
AS org_chart
FROM employees
START WITH first_name='Steven' AND last_name='King'
CONNECT BY PRIOR employee_id=manager_id;
```

#### EXPLAIN PLAN
```
  SET STATEMENT_ID = 'test1' FOR
    SELECT *
    FROM   employees e, departments d
    WHERE  e.department_id = d.department_id
    AND    e.last_name  = 'Mourgos';
   
-- Get the Test 1 results (feedback)

SELECT lpad(' ',level-1)||operation||' '||options||' '||
  object_name "Plan"
FROM plan_table
CONNECT BY prior id = parent_id
        AND prior statement_id = statement_id
  START WITH id = 0 AND statement_id = 'test1'
  ORDER BY id;
 
-- Test 2
EXPLAIN PLAN
SET STATEMENT_ID = 'test2' FOR
    SELECT *
    FROM   employees e
    WHERE  e.department_id = (SELECT department_id
                              FROM employees
                              WHERE last_name  = 'Mourgos');
                             
-- Get the Test 2 results (feedback)
SELECT lpad(' ',level-1)||operation||' '||options||' '||
  object_name "Plan"
FROM plan_table
CONNECT BY prior id = parent_id
        AND prior statement_id = statement_id
  START WITH id = 0 AND statement_id = 'test2'
  ORDER BY id;  
```
