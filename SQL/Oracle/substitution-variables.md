## SUBSTITUTION VARIABLES
Temporarily store values (& prompted every time) and (&& prompted once).

Used in WHERE, ORDER BY, column expressions, table names and entire SELECT statement.

Example:
```
SELECT * FROM employees
WHERE employee_id = &employee_num
WHERE job_id = ‘&job_title’  (use quotation marks for date and character values!)
ORDER BY &order_column;
```

#### DEFINE
Predefines substitution variables.

Example:
```
DEFINE employee_num = 200 
WHERE employee_id = &employee_num;    (user will not be prompted!)
Use UNDEFINE to delete && variable.
```

####VERIFY
Toggles the display of substitution variable on the screen for double check!
```
SET VERIFY ON
SELECT * FROM employees
WHERE employee_id = &employee_num;
```
