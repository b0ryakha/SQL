## Exercise 00
```sql
SELECT p.id, (SELECT COUNT(pv.id) FROM person_visits pv WHERE pv.person_id = p.id) AS "count_of_visits" FROM person p
ORDER BY count_of_visits DESC, p.id ASC
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/beb4a7ad-15d4-4392-a798-b0feddc5c4b6)

## Exercise 01
```sql
WITH tmp AS (
	SELECT p.name, (SELECT COUNT(pv.id) FROM person_visits pv WHERE pv.person_id = p.id) AS "count_of_visits" FROM person p
	ORDER BY count_of_visits DESC LIMIT 4
)

SELECT name FROM tmp ORDER BY name
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/ae9f3522-cdcf-4ef4-82e2-afe240c224cd)


## Exercise 02
```sql

```

## Exercise 03
```sql

```

## Exercise 04
```sql
WITH tmp_shit AS (
	SELECT p.id, COUNT(pv.id) AS "count_of_visits" FROM person p
	JOIN person_visits pv ON pv.person_id = p.id
	GROUP BY p.id
)

SELECT p.name, t.count_of_visits FROM person p
JOIN tmp_shit t ON t.id = p.id
WHERE t.count_of_visits > 3
GROUP BY p.name, t.count_of_visits
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/40c23e34-08fc-4a6b-ad7e-dde50501edde)

## Exercise 05
```sql
SELECT DISTINCT p.name FROM person p
LEFT JOIN person_visits pv ON pv.person_id = p.id
ORDER BY p.name
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/3b84c74e-71b2-406c-898c-0f5987fafa11)

## Exercise 06
```sql
SELECT p.name, COUNT(po.id) AS "count_of_orders", ROUND(AVG(m.price), 2) AS "average_price", MAX(m.price) AS "max_price", MIN(m.price) AS "min_price" FROM pizzeria p
JOIN menu m ON m.pizzeria_id = p.id
JOIN person_order po ON po.menu_id = m.id
GROUP BY p.name, m.price, m.pizza_name
ORDER BY m.pizza_name
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/3f22d412-67d9-41a4-9c2c-daa90cf3c760)

## Exercise 07
```sql
SELECT ROUND(AVG(p.rating), 4) AS "global_rating" FROM pizzeria p
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/3a0c03eb-3b9b-492f-a6e8-0642ec1b6839)

## Exercise 08
```sql

```

## Exercise 09
```sql
WITH tmp_shit AS (
	SELECT p.id, (MAX(p.age) - (MIN(p.age) / MAX(p.age))) AS "formula", ROUND(AVG(p.age), 2) AS "average" FROM person p
	GROUP BY p.id
)

SELECT p.address, t.formula, t.average, (t.formula > t.average) AS "comprasion" FROM person p
JOIN tmp_shit t ON t.id = p.id
ORDER BY p.address
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/0aef5a87-a716-4ef9-b8bf-69edbe0b0ee2)
