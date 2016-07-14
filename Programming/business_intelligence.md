##Business Intelligence

The business intelligence helps you to analyze the past and come up with strategies to improve the future.
A company generates raw data (mostly in databases). This raw data needs to be transformed into meaningful information that needs to be analyzed. The meaningful information is extracted using Business Intelligence (BI).

BI is an approach. It can be a technological approach or business process approach. A technological approach may be a tool or software application that helps extract meaningful information from a raw data. The components or types of functionality of the tool are as following:
-	Business Views. They can be past, current or predictive.
-	Business Performance Management. It uses Key Performance Indicators (KPI) or ratios to monitor health of the company.
-	Reporting includes online reports, online queries, or batch reports.

To make this components work, BI tool should rely on technical approaches:
-	Benchmarking – comparing your numbers with industry numbers.
-	Mining – determining a trend or discovering patterns.
-	Predictive Analysis – predicting future that based on the trends. 

The data comes from Online Transaction Processing System (OLTP). This system captures transactions very fast and on regular basis. The end users are clerks and low-level managers. Management uses a different system called Online Analytical Process System (OLAP) or Data Warehouse. This system is used for reports. The data is taken from OLTP, massaged and copied to OLAP.
In OLTP data is stored in tables (two-dimensional), but in OLAP data is stored in cubes (three-dimensional).

OLTP and OLAP represents structured data. It is only 10% of all data. Unstructured data, such as logs, chats, social media, and correspondence, also called Big Data represents 90% of all data.

#### BIG DATA
Big data is difficult to process by traditional system (send, view, or edit). Big Data (BD) is organization-specific. Traditional relational databases are not capable to handle BD. BD is usually measured by:
-	Velocity – the speed at which data comes in. (Collider - 40TB/sec.)
-	Volume – the data results in too large files to handle. (Facebook - 25TB/day)
-	Variety – data comes in different formats.
Big data tools:
Hadoop

#### NoSQL DATABASES
"Not Only SQL" databases (NoSQL) handle both structured and unstructured data and are useful to hold Big Data. They are relatively easy to use. They implement collections to store data, not tables like RDBMS and cubes for OLAP. The NoSQL databases may be categorized like:
-	Key-value store databases: Memcached, Coherence, Redis.
-	Tabular: BigTable (from Google), Hbase, Accumulo.
-	Document Oriented: MongoDB, Couch DB, Cloudant

Difference between NoSQL and RDBMS/OLAP.
To provide performance and scalability some RDBMS/OLAP features are omitted, thus NoSQL databases have less functionality:
-	No joins support.
-	No Complex Transactions support. They need to be implemented at application level.
-	No Constraints support (NOT NULL and others). They need to be implemented at application level.

Other query languages have support in NoSQL databases.

When to use NoSQL databases:
-	The ability to store and retrieve great quantities of data is important.
-	Storing relationships between the elements is not important.
-	Dealing with growing lists of elements (posts, logs).
-	The data is not structured or the structure is changing with time.
-	Prototypes or fast applications need to be developed.
-	Constraints and validations logic is not required to be implemented in database.

When NOT to use NoSQL databases:
-	Complex transactions need to be handled.
-	Joins must be handled by databases.
-	Validations must be handled by databases.

#### ADVANCED AGGREGATES
Daily Count uses date() function. To get the Daily Metrics we need the date. Most dates in databases are timestamps, which have hours and minutes, as well as the year, month, and day. Timestamps look like 2015-01-05 14:43:31, while dates are the first part: 2015-01-05. We can easily select the date an item was ordered at with the date function and the ordered_at field:
SELECT DATE(ordered_at)
FROM orders;
To limit the size of output use LIMIT 100 at the end of your query.
Orders Per Date uses date() and count() functions. 
SELECT COUNT(1)
FROM USERS;
This will treat all rows as a single group, and return one row in the result set - the total count. To count orders by their dates, we'll use the date and count functions and pair them with the group by clause. Together this will count the records in the table, grouped by date. For example, to see the user records counted by the date created, we use the date and count functions and group by clause as follows:
SELECT DATE(created_at), COUNT(1)
FROM USERS
GROUP BY DATE(created_at)
Daily Revenue uses date() and sum() functions. The data is usually taken from two tables and requires a join. Instead of using COUNT() function to count the rows per date, we'll use ROUND(SUM(amount_paid), 2) to add up the revenue per date. Note that the round() function rounds decimals to digits, based on the number passed in. Here round(..., 2) rounds the sum paid to two digits:
SELECT DATE(ordered_at), ROUND(SUM(amount_paid),2)
FROM orders
JOIN order_items ON orders.id = order_items.order_id
GROUP BY 1
ORDER BY 1;
With a small change, we can find out how much we're making per day for any single item:
SELECT DATE(ordered_at), ROUND(SUM(amount_paid),2)
FROM orders
JOIN order_items ON orders.id = order_items.order_id
WHERE name='smoothie'
GROUP BY 1
ORDER BY 1;
Percent of Revenue an Item Represents. To get the percent of revenue that each item represents, we need to know the total revenue of each item. We will later divide the per-item total with the overall total revenue.
The following query groups and sum the products by price to get the total revenue for each item. 
SELECT name, ROUND(SUM(amount_paid), 2)
FROM order_items
GROUP BY name
ORDER BY 2 DESC;
To calculate the percent, we'll need to get the total using a subquery. A subquery can perform complicated calculations and create filtered or aggregate tables on the fly. Subqueries are useful when you want to perform an aggregation outside the context of the current query. This will let us calculate the overall total and per-item total at the same time:
SELECT name, ROUND(SUM(amount_paid) /
  (SELECT SUM(amount_paid) FROM order_items) * 100.0, 2) AS PCT
FROM order_items
GROUP BY 1
ORDER BY 2 DESC;
Purchases by Category. We can group the items by the type they are. Since our order_items table does not include categories already, we'll need to make some. Previously we've been using GROUP BY with a column (like order_items.name) or a function (like date(orders.ordered_at)). We can also use GROUP BY with expressions. In this case a CASE statement is just what we need to build our own categories. Case statements are similar to if/else in other languages:
SELECT *,
  CASE name
    WHEN 'kale-smoothie'    THEN 'smoothie'
    WHEN 'banana-smoothie'  THEN 'smoothie'
    WHEN 'orange-juice'     THEN 'drink'
    WHEN 'soda'             THEN 'drink'
    WHEN 'blt'              THEN 'sandwich'
    WHEN 'grilled-cheese'   THEN 'sandwich'
    WHEN 'tikka-masala'     THEN 'dinner'
    WHEN 'chicken-parm'     THEN 'dinner'
     ELSE 'other'
  END AS category
FROM order_items
ORDER BY ID
LIMIT 100;
Now we can compute percentage by category. Here 1.0 * is a shortcut to ensure the database represents the percent as a decimal:
SELECT *,
CASE NAME
    WHEN 'kale-smoothie'    THEN 'smoothie'
    WHEN 'banana-smoothie'  THEN 'smoothie'
    WHEN 'orange-juice'     THEN 'drink'
    WHEN 'soda'             THEN 'drink'
    WHEN 'blt'              THEN 'sandwich'
    WHEN 'grilled-cheese'   THEN 'sandwich'
    WHEN 'tikka-masala'     THEN 'dinner'
    WHEN 'chicken-parm'     THEN 'dinner'
     ELSE 'other'
  END AS category, ROUND(1.0 * SUM(amount_paid) /
    (SELECT amount_paid FROM order_items) * 100, 2) AS pct
FROM order_items
GROUP BY 1
ORDER BY id
LIMIT 100;
Reorder Rate. We'll define reorder rate as the ratio of the total number of orders to the number of people making those orders. A lower ratio means most of the orders are reorders. A higher ratio means more of the orders are first purchases. Counting the total orders per product is straightforward. We count the distinct order_ids in the order_items table.
SELECT name, COUNT(DISTINCT order_id)
FROM order_items
GROUP BY 1
ORDER BY 1;
Now we need the number of people making these orders. To get that information, we need to join in the orders table and count unique values in the deliver_to field, and sort by the reorder_rate:
SELECT name, ROUND(1.0 * COUNT(distinct order_id) /
  COUNT(delivered_to), 2) AS reorder_rate
FROM order_items
JOIN orders ON orders.id = order_items.order_id
GROUP BY 1
ORDER BY 2 DESC;

COMMON BUSINESS QUERIES (METRICS)
As a data scientist, when you're not investigating spikes or dips in your data, you might be building dashboards of KPIs, or key performance indicators for a company. KPIs are often displayed on TVs on the walls of the office, and serve as high level health metrics for the business. While every company's metrics are defined slightly differently, the basics are usually very similar.
For our first KPI we'll calculate daily revenue. Daily Revenue is simply the sum of money made per day: 
SELECT DATE(created_at), ROUND(SUM(price), 2)
FROM purchases
GROUP BY 1
ORDER BY 1;
One way to easily create and organize temporary results in a query is with CTEs, Common Table Expressions, also known as with clauses. The WITH clauses make it easy to define and use results in a more organized way than subqueries:
  WITH {SUBQUERY_NAME} AS (
    {SUBQUERY_BODY}
  )
  SELECT ...
  FROM {SUBQUERY_NAME}
  WHERE ...

