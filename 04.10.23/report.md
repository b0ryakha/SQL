## Exercise 01
```sql
SELECT "id" FROM menu
EXCEPT
SELECT menu_id FROM person_order ORDER BY "id"
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/992fc609-09b1-44e1-9e10-9f53598f3770)

## Exercise 02
```sql
WITH identifiers AS (
	SELECT "id" FROM menu
	EXCEPT
	SELECT menu_id FROM person_order ORDER BY "id"
)

SELECT pizzeria.name, price FROM menu
JOIN pizzeria ON pizzeria.id = menu.pizzeria_id
WHERE pizzeria.id IN (SELECT * FROM identifiers)
ORDER BY pizza_name, price;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/aea1dfd7-7097-45c6-b638-06fedd4959f5)

## Exercise 03
```sql
SELECT pizzeria.name FROM pizzeria
WHERE (
	WITH necessary_persons AS (
		SELECT gender FROM person JOIN person_visits ON person.id = person_id
		WHERE pizzeria_id = pizzeria.id
	)
		
	SELECT COUNT(gender) FROM necessary_persons WHERE gender = 'female'
) != (
	WITH necessary_persons AS (
		SELECT gender FROM person JOIN person_visits ON person.id = person_id
		WHERE pizzeria_id = pizzeria.id
	)
		
	SELECT COUNT(gender) FROM necessary_persons WHERE gender = 'male'
)
ORDER BY pizzeria.name;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/23f84ba9-02fe-43dc-b122-1876ca219c71)

## Exercise 04
```sql
WITH men_orders AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN menu ON pizzeria.id = pizzeria_id
	JOIN person_order ON menu.id = menu_id
	JOIN person ON person.id = person_id
	WHERE gender = 'male'
),
women_orders AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN menu ON pizzeria.id = pizzeria_id
	JOIN person_order ON menu.id = menu_id
	JOIN person ON person.id = person_id
	WHERE gender = 'female'
)

(SELECT * FROM women_orders EXCEPT SELECT * FROM men_orders)
UNION
(SELECT * FROM men_orders EXCEPT SELECT * FROM women_orders)
ORDER BY "name";
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/3bad6033-46fe-4e3e-8fae-a2e20bf75997)

## Exercise 05
```sql

```
