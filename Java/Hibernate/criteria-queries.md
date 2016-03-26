## Criteria Queries
Hibernate provides alternate ways of manipulating objects and in turn data available in RDBMS tables. One of the methods is Criteria API which allows you to build up a criteria query object programmatically where you can apply filtration rules and logical conditions.

The Hibernate `Session` interface provides `createCriteria()` method which can be used to create a Criteria object that returns instances of the persistence object's class when your application executes a criteria query.
```java
Criteria criteria = session.createCriteria(Employee.class);
List results = criteria.list();
```
To get a single row use:
```
result (Employee) criteria.uniqueResult();
```

#### Restrictions with Criteria
You can use `add()` method available for Criteria object to add restriction for a criteria query:
```java
Criteria criteria = session.createCriteria(Employee.class);
criteria.add(Restrictions.eq("salary", 2000));
List results = criteria.list();
```
#### Criteria Queries
The Hibernate Session interface provides createCriteria() method which can be used to create a Criteria object that returns instances of the persistence object's class when your application executes a criteria query. Following is the simplest example of a criteria query is one which will simply return every object that corresponds to the Employee class.
```java
Criteria cr = session.createCriteria(Employee.class);
List results = cr.list();
```
Following are the few more examples covering different scenarios and can be used as per requirement:
```java
Criteria cr = session.createCriteria(Employee.class);

// To get records having salary more than 2000
cr.add(Restrictions.gt("salary", 2000));

// To get records having salary less than 2000
cr.add(Restrictions.lt("salary", 2000));

// To get records having fistName starting with zara
cr.add(Restrictions.like("firstName", "zara%"));

// Case sensitive form of the above restriction.
cr.add(Restrictions.ilike("firstName", "zara%"));

// To get records having salary in between 1000 and 2000
cr.add(Restrictions.between("salary", 1000, 2000));

// To check if the given property is null
cr.add(Restrictions.isNull("salary"));

// To check if the given property is not null
cr.add(Restrictions.isNotNull("salary"));

// To check if the given property is empty
cr.add(Restrictions.isEmpty("salary"));

// To check if the given property is not empty
cr.add(Restrictions.isNotEmpty("salary"));

// AND and OR operators:
Criterion salary = Restrictions.gt("salary", 2000);
Criterion name = Restrictions.ilike("firstNname","zara%");

// To get records matching with OR condistions
LogicalExpression orExp = Restrictions.or(salary, name);
cr.add( orExp );

// To get records matching with AND condistions
LogicalExpression andExp = Restrictions.and(salary, name);
cr.add( andExp );

List results = cr.list();

// Sorting results:
Criteria cr = session.createCriteria(Employee.class);
// To get records having salary more than 2000
cr.add(Restrictions.gt("salary", 2000));

// To sort records in descening order
crit.addOrder(Order.desc("salary"));

// To sort records in ascending order
crit.addOrder(Order.asc("salary"));

List results = cr.list();

// Projections & Aggregations:
Criteria cr = session.createCriteria(Employee.class);
// To get total row count.
cr.setProjection(Projections.rowCount());

// To get average of a property.
cr.setProjection(Projections.avg("salary"));

// To get distinct count of a property.
cr.setProjection(Projections.countDistinct("firstName"));

// To get maximum of a property.
cr.setProjection(Projections.max("salary"));

// To get minimum of a property.
cr.setProjection(Projections.min("salary"));

// To get sum of a property.
cr.setProjection(Projections.sum("salary"));
```

#### Pagination
There are two methods of the Criteria interface for pagination:

Method |	Description |
--- | --- |
public Criteria setFirstResult(int firstResult) | This method takes an integer that represents the first row in your result set, starting with row 0. |
public Criteria setMaxResults(int maxResults) | This method tells Hibernate to retrieve a fixed number maxResults of objects. |

Using above two methods together, we can construct a paging component in our web or Swing application. Following is the example which you can extend to fetch 10 rows at a time:
```java
Criteria cr = session.createCriteria(Employee.class);
cr.setFirstResult(1);
cr.setMaxResults(10);
List results = cr.list();
```

#### Sorting the Results
The Criteria API provides the `org.hibernate.criterion.Order` class to sort your result set in either ascending or descending order, according to one of your object's properties. This example demonstrates how you would use the Order class to sort the result set:
```java
Criteria cr = session.createCriteria(Employee.class);
// To get records having salary more than 2000
cr.add(Restrictions.gt("salary", 2000));

// To sort records in descening order
crit.addOrder(Order.desc("salary"));

// To sort records in ascending order
crit.addOrder(Order.asc("salary"));

List results = cr.list();
```

#### Projections & Aggregations:
The Criteria API provides the `org.hibernate.criterion.Projections` class which can be used to get average, maximum or minimum of the property values. The Projections class is similar to the Restrictions class in that it provides several static factory methods for obtaining Projection instances.
```java
Criteria cr = session.createCriteria(Employee.class);

// To get total row count.
cr.setProjection(Projections.rowCount());

// To get average of a property.
cr.setProjection(Projections.avg("salary"));

// To get distinct count of a property.
cr.setProjection(Projections.countDistinct("firstName"));

// To get maximum of a property.
cr.setProjection(Projections.max("salary"));

// To get minimum of a property.
cr.setProjection(Projections.min("salary"));

// To get sum of a property.
cr.setProjection(Projections.sum("salary"));
```

#### Fetch Random Rows
To fetch some random rows from the result set use the following:
```java
Criteria criteria = session.createCriteria(YourTable.class);
criteria.add(Restrictions.eq('yourFieldVariable', anyValue));
criteria.add(Restrictions.sqlRestriction("1=1 order by rand()"));
criteria.setMaxResults(5);
return criteria.list();
```
The `Restrictions.sqlRestriction` will add keyword AND so to nullify its effect, we shall add a dummy condition and inject our `rand()` function.
