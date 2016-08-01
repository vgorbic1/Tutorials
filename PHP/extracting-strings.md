## Extracting strings from texts

#### Ending an extract on a complete word.
To end an extract on a complete word, you need to find the final space, and use that to determine the length of th esubstring. Use SQL query to get first, say 100 characters:
```sql
SELECT article_id, title, LEFT(article, 100) AS first100 
FROM journal ORDER BY created DESC;
```
```php
$extract = $row['first100'];
// find position of last space in extract
$lastSpace = strrpos($extract, ' ');
// use $lastspace to set lingth of new extract and a ...
echo substr($extract, 0, $lastSpace) . '...';
```

#### Extracting the first paragraph
```sql
SELECT article_id, title, article
FROM journal ORDER BY created DESC;
```
```php
echo substr($row['article'], 0, strpos($row['article'], "\n"));
```
