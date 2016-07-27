## JOINS

#### CARTESIAN JOINS
A.k.a. Cartesian product, a.k.a. Cross Join. Each record in the first table matches a record in another table. Mostly used for data analysis. Number of rows in the first table multiplied by number of rows in the second table. Happen when the condition is invalid or omitted.

Traditional method:
```
SELECT isbn, title, location, ‘ ‘ Count
FROM books, warehouses
ORDER BY location, title;
```

JOIN method:

Use CROSS keyword.
```
SELECT isbn, title, location, ‘ ‘ Count
FROM books CROSS JOIN warehouses
ORDER BY location, title;
```

#### EQUALITY JOINS
A.k.a. equijoins, a.k.a. inner joins, a.k.a. simple joins. Use a common column to join tables. Results should include whenever there is a match between the columns.
The keyword JOIN may go with INNER. It is by default and may be omitted. Just use JOIN alone.

Traditional method:

Use WHERE clause to join tables.
```
SELECT title, name
FROM books, publisher
WHERE books.pubid  = publisher.pubid;   
```
(here books and publisher are “column qualifiers”)
```
SELECT title, books.pubid, name
FROM books, publisher
WHERE books.pubid = publisher.pubid AND publisher.pubid = 4;
```
With aliases:

```
SELECT b.title, b.pubid, p.name
FROM book b, publisher p
WHERE b.pubid = p.pubid AND (b.cost < 15 OR p.pubid = 1)
ORDER BY title;
```

With four tables:
```
SELECT c.lastname, c.firstname, b.title
FROM customers c, orders o, orderitems oi, books b
WHERE c.customer# = o.customer# AND o.order# = oi.order# AND oi.sbn = b.isbn AND category = ‘COMPUTER’
ORDER BY lastname, firstname;
```

JOIN method:

With NATURAL JOIN, that creates join automatically:
```
SELECT title, pubid, name
FROM publisher NATURAL JOIN books; (no qualifiers for the common column!)
```
```
SELECT b.isbn, p.name (qualifiers may be used here, but no qualifiers for the common column!)
FROM books b NATURAL JOIN publisher p;
```
With JOIN and USING():
```
SELECT b.title, pubid, p.name
FROM publisher p JOIN books B USING(pubid); (no qualifiers for the column within USING keyword or error!)
```
Multiple tables with USING:
```
SELECT c.lastname, c.firstname,b.title
FROM customers c JOIN orders o USING (customer#)
	JOIN orderitems oi USING (order#)
	JOIN books b USING (isbn)
WHERE category = ‘COMPUTER’
ORDER BY lastname, firstname;
```
If there are no commonly named columns use ON keyword:
```
SELECT b.title, b.pubid, p.name (qualifiers may be omitted)
FROM publisher2 p JOIN books b ON p.id = b.pubid (shared same column but named differently!)
```
To add additional conditions use AND or WHERE.

#### NON-EQUALITY JOINS
When columns cannot be joined with an equal sign. Gives ability to store the range’s minimum value in one column and maximum in the other column.

Traditional way:

To determine the range use BETWEEN operator:
```
SELECT b.title, p.gift
FROM books b, promotion p
WHERE b.retail BETWEEN p.minretail AND p.maxretail;
```

Three tables:
```
SELECT UNIQUE b.title, o.paideach, p.gift (use UNIQUE or DISTINCT to take only one name of the book)
FROM orderitems o, books b , promotion p
WHERE o.isbn = b.isbn AND (o.paideach BETWEEN p.minretail AND p.maxretail);
```

With comparison operators:
```
SELECT title, gift
FROM books, promotion
WHERE retail >= minretail AND retail <= maxretail;
```

JOIN method:
```
SELECT b.title, p.gift
FROM books b JOIN promotion p ON b.retail 
BETWEEN p.minretail AND p.maxretail;
```

#### SELF-JOINS
Used to get the data from the same table.

Traditional method:
```
SELECT r.firstname, r.lastname, c.lastname "Referred"
FROM customers c, customers r
WHERE c.referred = r.customer#; (columns have similar data!)
```

JOIN method:
```
SELECT r.firstname, r.lastname, c.lastname "Referred"
FROM customers c JOIN customers r ON c.referred = r.customer#; (USING cannot be used!)
```

#### OUTER JOINS
List all data including NULL. By default JOIN keyword creates inner join. To make it outer join use LEFT JOIN, RIGHT JOIN, or FULL JOIN. (or use LEFT OUTER JOIN, RIGHT OUTER JOIN, but not!!! FULL OUTER JOIN)

Traditional method:
```
SELECT c.lastname, c.firstname, o.order#
FROM customers c, orders o
WHERE c.customer# = o.customer#(+); 
```
+ sign is required to show all NULL values in this column in this  “deficient” table and can be placed only one time! Cannot use IN or OR operators here! Shows all unmatched records for the “customers” table. Same as using LEFT OUTER JOIN keywords.

Join Method:

Using ON keyword:
```
SELECT c.lastname, c.firstname, o.order#
FROM customers c LEFT OUTER JOIN orders o ON c.customer#=o.customer#
ORDER BY c.lastname, c.firstname;
```

Using USING keyword:
```
SELECT c.lastname, c.firstname, o.order#
FROM customers c LEFT OUTER JOIN orders o USING (customer#)
ORDER BY c.lastname, c.firstname;
```
