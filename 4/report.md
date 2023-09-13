## 1)
```sql
SELECT "id", "pizza_name" FROM "menu"
UNION
SELECT "id", "name" FROM "person" ORDER BY "id", "pizza_name"
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/a9862ce6-8151-4d81-b7ce-7507c87008a6)

## 2)
```sql
SELECT "pizza_name" FROM "menu"
UNION
SELECT "name" FROM "person" ORDER BY "pizza_name"
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b3d348b2-0d7d-4e89-9371-9506500deb2d)

## 3)
```sql
SELECT "person_id" FROM "person_order" WHERE "order_date"
IN (SELECT "visit_date" FROM "person_visits" WHERE person_order.person_id = person_visits.person_id)
ORDER BY "order_date" DESC
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/9e4f0722-cf2f-4568-87f3-218175f6d3f6)

## 4)
```sql
SELECT ABS(
	(SELECT COUNT("person_id") FROM "person_order" WHERE "order_date" = '2022-01-07')
	-
	(SELECT COUNT("person_id") FROM "person_visits" WHERE "visit_date" = '2022-01-07')
)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/678b32dc-af4e-4855-ac0f-534224f765bc)
