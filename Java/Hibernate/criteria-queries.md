## Criteria Queries


#### Fetch Random Rows
To fetch some random rows from the result set use the following:
```java
Criteria criteria = session.createCriteria(YourTable.class);
criteria.add(Restrictions.eq('yourFieldVariable', anyValue));
criteria.add(Restrictions.sqlRestriction("1=1 order by rand()"));
criteria.setMaxResults(5);
return criteria.list();
```
Any Restrictions.sqlRestriction will add keyword 'and' so to nullify its effect, we shall add a dummy condition and inject our rand() function.
