## Exercise 00
```sql
DROP VIEW IF EXISTS v_males, v_females;

CREATE VIEW v_males AS
	SELECT * FROM person WHERE gender = 'male';
	
CREATE VIEW v_females AS
	SELECT * FROM person WHERE gender = 'female';
	
SELECT * FROM v_males, v_females;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b6ca6df6-c9df-4e8f-b405-6d7582e39c4f)

## Exercise 01
```sql
DROP VIEW IF EXISTS v_males, v_females;

CREATE VIEW v_males AS
	SELECT * FROM person WHERE gender = 'male';
	
CREATE VIEW v_females AS
	SELECT * FROM person WHERE gender = 'female';

SELECT "name" FROM v_males
UNION
SELECT "name" FROM v_females
ORDER BY "name";
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b1d28390-9505-4395-9a74-d5b563b647ab)


## Exercise 02
```sql
DROP VIEW IF EXISTS v_generated_dates;

CREATE VIEW v_generated_dates AS
	SELECT generate_series('01.01.2022', '31.01.2022', interval '1 day')::date AS generated_date
	ORDER BY generated_date;

SELECT * FROM v_generated_dates;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/27385d3d-88b2-4e97-974f-0b9df8b919f8)


## Exercise 03
```sql
DROP VIEW IF EXISTS v_generated_dates;

CREATE VIEW v_generated_dates AS
	SELECT generate_series('01.01.2022', '31.01.2022', interval '1 day')::date AS generated_date
	ORDER BY generated_date;

SELECT generated_date FROM v_generated_dates
LEFT JOIN person_visits ON generated_date = visit_date
WHERE visit_date IS NULL;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/dfdc07db-8d52-466f-b13b-4eb595fb0ba0)

## Exercise BONUS LEVEL
```sql
SELECT p1.name, p2.name, p1.address FROM person p1
JOIN persons2 p2 ON p1.address = p2.address
WHERE p1.id < p2.id;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/11ef939f-be27-473c-9712-44ba2e5d057d)


## Exercise 04
```sql
DROP VIEW IF EXISTS v_R, v_S, v_symmetric_union;

CREATE VIEW v_R AS
	SELECT "id" FROM person_visits WHERE visit_date = '2022-01-02';
	
CREATE VIEW v_S AS
	SELECT "id" FROM person_visits WHERE visit_date = '2022-01-06';
	
CREATE VIEW v_symmetric_union AS
	(SELECT * FROM v_R EXCEPT SELECT * FROM v_S)
	UNION
	(SELECT * FROM v_S EXCEPT SELECT * FROM v_R);

SELECT * FROM v_symmetric_union ORDER BY "id";
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/53730419-df69-4477-9aa3-fa09822edc0e)

## Exercise 05
```sql
DROP VIEW IF EXISTS v_price_with_discount;

CREATE VIEW v_price_with_discount AS
	SELECT p.name, m.pizza_name, m.price, round(SUM(m.price * 0.9)) AS discount_price FROM person_order po
	JOIN person p ON p.id = po.person_id
	JOIN menu m ON m.id = po.menu_id
	GROUP BY p.name, m.pizza_name, m.price
	ORDER BY p.name;
	
SELECT * FROM v_price_with_discount;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/3273c22e-5903-456f-98cc-7d816c31af0e)

## Exercise 06
```sql
DROP MATERIALIZED VIEW IF EXISTS mv_dmitriy_visits_and_eats;

CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats AS
	SELECT pi.name FROM person_visits pv
	JOIN pizzeria pi ON pi.id = pv.pizzeria_id
	JOIN menu m ON m.pizzeria_id = pv.pizzeria_id
	JOIN person p ON pv.person_id = p.id
	WHERE p.name = 'Dmitriy' AND pv.visit_date = '2022-01-08' AND m.price < 800;
	
SELECT * FROM mv_dmitriy_visits_and_eats;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/c023131e-bd4b-4693-9798-6142cf335d66)

## Exercise 07
```sql
DROP MATERIALIZED VIEW IF EXISTS mv_dmitriy_visits_and_eats;

DELETE FROM person_visits pv
WHERE pv.id = 20;

CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats AS
	SELECT pi.name FROM person_visits pv
	JOIN pizzeria pi ON pi.id = pv.pizzeria_id
	JOIN menu m ON m.pizzeria_id = pv.pizzeria_id
	JOIN person p ON pv.person_id = p.id
	WHERE p.name = 'Dmitriy' AND pv.visit_date = '2022-01-08' AND m.price < 800;

INSERT INTO person_visits(id, person_id, pizzeria_id, visit_date)
VALUES (20, 9, 3, '2022-01-08');

REFRESH MATERIALIZED VIEW mv_dmitriy_visits_and_eats;

SELECT * FROM mv_dmitriy_visits_and_eats;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/c676d614-f99f-4e56-97e1-4a8c44282d6d)
