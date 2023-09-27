## 1)
```sql
SELECT * FROM person, pizzeria ORDER BY person.id, pizzeria.id
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/6a0ddb32-2b49-4feb-bcc9-e735741d58df)

## 2)
```sql
SELECT person_visits.visit_date AS action_date, person.name FROM person_visits, person
WHERE person_visits.visit_date IN (SELECT order_date FROM person_order)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/fa5fd2e2-53e2-47cb-bbd0-c36d0e47dbba)

## 3)
```sql
SELECT order_date, (person.name || ' (age: ' || person.age || ')') AS person_info FROM person_order
JOIN person ON person_order.person_id = person.id
ORDER BY order_date, person_info
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/f361dda3-e760-44da-a50e-de4741e7fb8f)

## 4)
```sql
SELECT order_date, (person.name || ' (age: ' || person.age || ')') AS person_info FROM person_order
NATURAL JOIN person ORDER BY order_date, person_info
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b80617dc-4c7d-42f9-89fd-3b692ef26adb)

## 5)
```sql
SELECT pizzeria.name FROM pizzeria
WHERE pizzeria.id NOT IN (SELECT pizzeria_id FROM person_visits);

SELECT pizzeria.name FROM pizzeria
WHERE NOT EXISTS (SELECT pizzeria_id FROM person_visits WHERE pizzeria_id = pizzeria.id);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b22a02d3-6fb9-486b-9cf2-67509af99519)

## 6)
```sql
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name FROM person, pizzeria
JOIN menu ON pizzeria.id = menu.pizzeria_id
ORDER BY person_name, menu.pizza_name, pizzeria_name;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/fda428d2-78f7-44c9-8253-f7fe3a074dd8)
