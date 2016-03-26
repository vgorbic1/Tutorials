## Criteria Queries
Hibernate provides alternate ways of manipulating objects and in turn data available in RDBMS tables. One of the methods is Criteria API which allows you to build up a criteria query object programmatically where you can apply filtration rules and logical conditions.

The Hibernate `Session` interface provides `createCriteria()` method which can be used to create a Criteria object that returns instances of the persistence object's class when your application executes a criteria query.
```java
Criteria criteria = session.createCriteria(Employee.class);
List results = criteria.list();
```

#### Restrictions with Criteria
You can use `add()` method available for Criteria object to add restriction for a criteria query:
```java
Criteria criteria = session.createCriteria(Employee.class);
criteria.add(Restrictions.eq("salary", 2000));
List results = criteria.list();
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
