##SUBQUERIES
Subquery is one complete query inside another. If subquery output consists of only one row it is a single-row subquery, if several rows – multiple-row subquery. If multiple columns are involved – multiple column subquery.
Most commonly used in WHERE or HAVING clauses; rare in SELECT and FROM clauses. 
- A subquery must be a complete query itself.
- A subquery cannot have ORDER BY clause, except in FROM clause.
- A subquery must be enclosed in parenthesis.
- A subquery in WHERE or HAVING may be only on the right side of the comparison operator.
- A subquery can be nested to a depth of 255 subqueries in WHERE and with no limit in FROM clause. 

#### SINGLE-ROW SUBQUERIES
If you need an unknown result from only single value in only one column!

Use operators: =, <, >, <=, >=, <>, !=, IN.

Example1:
```
SELECT category, title, cost 
FROM books
WHERE cost > (SELECT cost 
   FROM books 
   WHERE title='DATABASE IMPLEMENTATION')
AND category = 'COMPUTER';
```
Example2:
```
SELECT category, AVG(retail-cost) 
FROM books 
GROUP BY category HAVING AVG(retail-cost) > (SELECT AVG(retail-cost) 
 FROM books 
 WHERE category = ‘LITERATURE’);
```
To make the result of a subquery available for each row in column use the subquery in SELECT clause:
```
SELECT title, retail, (SELECT TO_CHAR(AVG(retail), 999.99) 
 FROM books) "Overall Average"
FROM books;
```

#### MULTIPLE-ROW SUBQUERIES
Return more than one row. Mostly used in WHERE and HAVING clauses. Do not use single row comparison operators (< , >, = and so on)! Use IN ALL or ANY.

Example:
```
SELECT title, retail, category 
FROM books
WHERE retail IN (SELECT MAX(retail) 
FROM books 
GROUP BY category)
ORDER BY category;
```
To treat subquery as a set of values use ALL, ANY (SOME is an equivalent to ANY) or NOT:

- >ALL – More than the highest value returned (same as MAX() function in a single-row subquery)
- <ALL – Less than the lowest value returned
- >ANY – More than the lowest value returned
- <ANY – Less than the highest value returned
- =ANY – Is the same as IN
- <>ALL – is the same as NOT IN

Example:
```
SELECT title, retail 
FROM books
WHERE retail <ALL (SELECT retail 
        FROM books 
        WHERE category = 'COOKING'); 
```
It shows book priced less than the lowest in the subquery.

Example2:
```
SELECT title, retail 
FROM books
WHERE retail <ANY (SELECT retail 
                   FROM books 
                   WHERE category = 'COOKING'); 
```
It shows books priced less than the highest in the subquery.

To modify the statement so that other books do not show use WHERE <> ‘COOKING’ in the outer query.

If subquery returns multiple results to grouped outer query use HAVING:

Example:
```
SELECT order#, SUM(quantity*paideach) 
FROM orderitems
GROUP BY order#
HAVING SUM(quantity*paideach)>ALL (SELECT SUM(quantity*paideach) 
                                   FROM customers JOIN orders USING(customer#) 
                                     JOIN orderitems USING(order#) 
                                   WHERE state = 'FL' 
                                   GROUP BY order#);
```

#### NULL VALUES IN SUBQUERIES
Use NVL() to include NULL values, but the substitution must occur in both outer and subqueries and the value submitted instead NULL in NVL() must be one that couldn’t possibly exist anywhere else in that column.

Example:
```
SELECT customer# 
FROM customers
WHERE NVL(referred,0) = (SELECT NVL(referred,0) 
                         FROM customers 
                         WHERE customer# = 1005);
```
Example without NVL():
```
SELECT DISTINCT title 
FROM books JOIN orderitems USING(isbn)
WHERE order# IN (SELECT order# 
                 FROM orders 
                 WHERE shipdate IS NULL);
```

#### NESTED SUBQUERIES
Example:
```
SELECT customer#, lastname, firstname 
FROM customers JOIN orders USING(customer#)
WHERE order# IN (SELECT order# 
                 FROM orderitems 
                 GROUP BY order# 
                 HAVING COUNT(*) = (SELECT MAX(count(*)) 
                                    FROM orderitems 
                                    GROUP BY order#));
MULTIPLE-COLUMN SUBQUERIES
```
Combine duplicate WHERE conditions into a single WHERE clause.

#### PAIRWISE COMPARISON SUBQUERY
Display the details of the employees who are managed by the same manager and work in the same department as
employees with the first name of “John.”
```
SELECT employee_id, manager_id, department_id
FROM empl_demo
WHERE (manager_id, department_id) IN
          (SELECT manager_id, department_id
           FROM empl_demo
           WHERE first_name = 'John')
AND first_name <> 'John';
```

#### NONPAIRWISE COMPARISON SUBQUERY
Display the details of the employees who are managed by the same manager as the employees with the first name of “John” and work in the same department as the employees with the first name of “John.”
```
SELECT employee_id, manager_id, department_id
FROM empl_demo
WHERE manager_id IN
          (SELECT manager_id
           FROM empl_demo
           WHERE first_name = 'John')
AND department_id IN
          (SELECT department_id
           FROM empl_demo
           WHERE first_name = 'John')
AND first_name <> 'John';
```
#### SCALAR SUBQUERY
A scalar (single result) subquery expression is a subquery that returns exactly one column value from one row.
Scalar subqueries can be used in the condition and expression part of DECODE and CASE, in all clauses of SELECT except GROUP BY, and in the SET clause and WHERE clause of an UPDATE statement.
If the subquery returns 0 rows, the value of the scalar subquery expression is NULL. If the subquery returns more than one row, the Oracle returns an error.

Example 1:
```
SELECT employee_id, last_name,(CASE
  WHEN department_id = (SELECT department_id
                        FROM departments
                        WHERE location_id = 1800)
  THEN 'Canada' ELSE 'USA' END) location
FROM employees;
```
Example 2:
```
SELECT employee_id, last_name
FROM employees e
ORDER BY (SELECT department_name
          FROM departments d
          WHERE e.department_id = d.department_id);
```

#### CORRELATED SUBQUERIES
Used for row-by-row processing. Each subquery is executed once for every row of the outer query.

Example 1: Find all employees who earn more than the average salary in their department.
```
SELECT last_name, salary, department_id
FROM employees outer
WHERE salary > (SELECT AVG(salary)
                FROM employees
                WHERE department_id = outer.department_id); (Each time a row from the outer query is processed, the inner query is evaluated.)
```
Example 2: Display details of those employees who have changed jobs at least twice.
```
SELECT e.employee_id, last_name, e.job_id
FROM employees e
WHERE 2 <= (SELECT COUNT(*)
            FROM job_history
            WHERE employee_id = e.employee_id);
```
####EXISTS
The EXISTS operator tests for existence of rows in the results set of the subquery. If a subquery row value is found, the search does not continue in the inner query and the condition is flagged TRUE. If a subquery row value is not found, the condition is flagged FALSE and the search continues in the inner query. NOT EXISTS is an alternative to EXISTS.

Example: Find All Departments That Do Not Have Any Employees
```
SELECT department_id, department_name
FROM departments d
WHERE NOT EXISTS (SELECT 'X' (we do not interested in data! Don’t care!)
                  FROM employees
                  WHERE department_id = d.department_id);
```

#### WITH
Using the WITH clause, you can use the same query block in a SELECT statement when it occurs more than once within a complex query. The WITH clause retrieves the results of a query block and stores it in the user’s temporary tablespace. The WITH clause may improve performance.

Example:
```
WITH
dept_costs AS (SELECT d.department_name, SUM(e.salary) AS dept_total
               FROM employees e JOIN departments d
               ON e.department_id = d.department_id
               GROUP BY d.department_name),
avg_cost AS (SELECT SUM(dept_total)/COUNT(*) AS dept_avg
             FROM dept_costs) (do not execute again, just use one above that is saved instead)
SELECT * FROM dept_costs
WHERE dept_total >
       (SELECT dept_avg (do not execute again, just use one above that is saved instead)
        FROM avg_cost) (do not execute again, just use one above that is saved instead)
        ORDER BY department_name;
```
