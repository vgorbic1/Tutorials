## Grouping

### GROUP BY
Allows to select non-aggregate columns and aggregate functions. If there is an aggregate function and non-aggregate columns in SELECT statement, add all non-aggregate columns in GROUP BY column.
Columns used to group data in the GROUP BY clause don’t have to be listed in SELECT clause.

No column aliases in GROUP BY clause!

Results are displayed in ascending order of the columns listed in GROUP BY clause. To sort them differently use ORDER BY clause.

Example:
```
SELECT category AVG(retail-cost) “Profit” 
FROM books 
GROUP BY category;
```

#### HAVING
This clause is used to restrict the groups returned bay a query. If you need to use a group function to restrict groups, you must use the HAVING clause, since WHERE cannot contain aggregate functions. HAVING can precede GROUP BY clause, but it is illogical. It is better to have HAVING after GROUP BY.
HAVING specifies which groups are displaying in the results.  It is just like WHERE, but for aggregate data.
Use AND OR NOT logical operators with HAVING.

Example: 
```
SELECT category, AVG(retail-cost) “Profit” 
FROM books 
GROUP BY category HAVING AVG(retail-cost) > 15;
```

Example:
```
SELECT category, AVG(retail-cost) “Profit” 
FROM books 
WHERE pubdate > ’01-JAN-05’ 
GROUP BY category HAVING AVG(retail-cost) > 15;
```

#### ROLLUP
Produces cumulative aggregates, such as subtotals. The cumulative aggregates can be used in reports, charts, and graphs. The ROLLUP operator creates subtotals that roll up from the most detailed level to a grand total, following the grouping list specified in the GROUP BY clause. 

Example:
```
SELECT department_id, job_id, SUM(salary)
FROM employees
WHERE department_id < 60
GROUP BY ROLLUP(department_id, job_id);
```

#### CUBE
Produces cross-tabulation values with a single SELECT statement. ROLLUP produces only a fraction of possible subtotal combinations, whereas CUBE produces subtotals for all possible combinations of groupings specified in the GROUP BY clause, and a grand total.

Example:
```
SELECT department_id, job_id, SUM(salary)
FROM employees
WHERE department_id < 60
GROUP BY CUBE (department_id, job_id);
```

#### GROOPING()
The GROUPING function is used with either the CUBE or ROLLUP operator to find the groups forming the subtotal in a row. It is used to differentiate stored NULL values from NULL values created by ROLLUP or CUBE and returns 0 or 1.

Example:
```
SELECT department_id DEPTID, job_id JOB, SUM(salary), 
   GROUPING(department_id) GRP_DEPT, (if it is a grouping cell it writes 1, otherwise it writes 0)
   GROUPING(job_id) GRP_JOB
FROM employees
WHERE department_id < 50
GROUP BY ROLLUP(department_id, job_id);
```

#### GROUPING SETS

The GROUPING SETS syntax is used to define multiple groupings in the same query. All groupings specified in the GROUPING SETS clause are computed and the results of individual groupings are combined with a UNION ALL operation. Grouping set is efficient because only one pass over the base table is required, there is no need to write complex UNION statements and the more elements GROUPING SETS has, the greater is the performance benefit.

Example:
```
SELECT department_id, job_id, manager_id,AVG(salary)
FROM employees
GROUP BY GROUPING SETS((department_id,job_id), (job_id,manager_id));
```
