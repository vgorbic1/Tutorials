##Find and Replace data in MySQL database.
This is an example with a WordPress database to replace all data (in all rows) in column *guid* that has *madisontalkers* with *madisontalks*: 
```sql
UPDATE wp_posts SET guid = REPLACE(guid, 'madisontalkers', 'madisontalks') 
WHERE guid LIKE '%madisontalkers%';
```
