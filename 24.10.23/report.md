## Exercise 00:
```sql
SELECT p.id, (SELECT COUNT(pv.id) FROM person_visits pv WHERE pv.person_id = p.id) AS "count_of_visits" FROM person p
ORDER BY count_of_visits DESC, p.id ASC
```
![Uploading image.png…]()

