##Set Operators
Set operators combine the results of two or more component queries into one result. The selection in SELECT must match both queries in number of columns and data type. Set operators may be used in subqueries. By default ordered in ascending order of the first column in the first query. Use dummy columns to display those columns that are not presented in one of the compound queries.

#### UNION
Return all rows from both queries after eliminating duplicates. Number of columns and data types should be the same in both queries. NULL values not ignored.

Syntax:
```
SELECT expression1, expression2, ... expression_n
FROM tables
WHERE conditions
UNION
SELECT expression1, expression2, ... expression_n
FROM tables
WHERE conditions;
```
Example:
```
SELECT employee_id, job_id FROM employees
UNION 
SELECT employee_id, job_id FROM job_history;
```
The ORDER BY can appear only once at the end of the compound query and they recognize only the columns from the first compound query. They accept column names, numbers, or aliases. 

Example 2:
```
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id <= 500
UNION
SELECT company_id, company_name
FROM companies
WHERE company_name = 'Apple'
ORDER BY 2; (here 2 is the second column in the list of columns)
```

#### UNION ALL
Return all rows with all duplicates.  

Example:
```
SELECT employee_id, job_id FROM employees
UNION ALL
SELECT employee_id, job_id FROM job_history;
```

#### INTERSECT
Returns all rows that are common to multiple queries. Does not ignore NULL values.

Example:
```
SELECT employee_id, job_id FROM employees
INTERSECT
SELECT employee_id, job_id FROM job_history;
```

#### MINUS
Returns all distinct rows selected by the first query, but not present in the second query set (remaining).

Example:
```
SELECT employee_id, job_id FROM employees
MINUS
SELECT employee_id, job_id FROM job_history;
```
Use of dummy column for char datatype:
```
SELECT employee_id, job_id “job” FROM employees
UNION 
SELECT employee_id, TO_CHAR(NULL) “job” FROM job_history;
```
Use of dummy column for number datatype:
```
SELECT employee_id, job_id FROM employees
UNION 
SELECT employee_id, 0 FROM job_history;
```
