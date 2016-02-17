## Interview Questions

**What is the difference between a JOIN and UNION?**

Joins and Unions can be used to combine data from one or more tables.  The difference lies in how the data is combined. Whereas a join is used to combine columns from different tables, the union is used to combine rows:

JOIN

![join](https://cloud.githubusercontent.com/assets/13823751/12952637/bdc938de-cfdc-11e5-9750-46e64888ec23.png)

UNION

![union](https://cloud.githubusercontent.com/assets/13823751/12952644/c0e67644-cfdc-11e5-892c-d01e0199e103.png)

SOURCE: [Kris Wenzel](http://www.essentialsql.com/what-is-the-difference-between-a-join-and-a-union/)

**How can we find the current date using mysql?**

Use `CURDATE()` function

**How can we know the number of days between two given dates using mysql?**

Use standard SQL `DATEDIFF()` function with two dates as parameters.

**What are the differences between drop, delete, and truncate a table commands?**
- DELETE command is used to remove rows from a table. It is a DML command and can be rolled back.
- TRUNCATE removes all rows from a table. It is a DDL command, so the operation cannot be rolled back. TRUCATE is faster and doesn't use as much undo space as a DELETE.
- DROP command removes a table from the database. All the tables' rows, indexes and privileges will also be removed. It is the DDL command, so the operation cannot be rolled back.


