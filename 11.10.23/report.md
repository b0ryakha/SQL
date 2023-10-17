## Exercise 00
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_menu_pizzeria_id, idx_person_visits_person_id, idx_person_visits_pizzeria_id, idx_person_order_person_id, idx_person_order_menu_id;

CREATE INDEX idx_menu_pizzeria_id ON menu(pizzeria_id);
CREATE INDEX idx_person_visits_person_id ON person_visits(person_id);
CREATE INDEX idx_person_visits_pizzeria_id ON person_visits(pizzeria_id);
CREATE INDEX idx_person_order_person_id ON person_order(person_id);
CREATE INDEX idx_person_order_menu_id ON person_order(menu_id);
```


## Exercise 01
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_menu_pizzeria_id;
CREATE INDEX idx_menu_pizzeria_id ON menu(pizzeria_id);

EXPLAIN ANALYZE
SELECT pizzeria_id FROM menu;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/6de4d730-b12e-4aed-a241-ca0ac1956465)


## Exercise 02
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_person_name;
CREATE INDEX idx_person_name ON person("name");

EXPLAIN ANALYZE
SELECT UPPER("name") FROM person;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/9c1c811f-7a58-43d6-a087-9c42147af861)
![image](https://github.com/b0ryakha/SQL/assets/47691726/605a2347-a897-45aa-9a21-f1a33d1dfbca)


## Exercise 03
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_person_order_multi;
CREATE INDEX idx_person_order_multi ON person_order(person_id, menu_id);

EXPLAIN ANALYZE
SELECT person_id, menu_id, order_date
FROM person_order
WHERE person_id = 8 AND menu_id = 19;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/f08170d9-76d9-4081-b48e-d4a6e4c6966b)
![image](https://github.com/b0ryakha/SQL/assets/47691726/54102138-2e39-4fc9-9ec9-b1152244dcc2)

## Exercise 04
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_menu_unique;
CREATE UNIQUE INDEX idx_menu_unique ON menu(pizzeria_id, pizza_name);

EXPLAIN ANALYZE
SELECT pizzeria_id, pizza_name FROM menu;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/c16c2889-1d84-4e48-811e-ea03acdda69b)
![image](https://github.com/b0ryakha/SQL/assets/47691726/ed458779-ed61-4dd2-b7d7-663a5a7eafe5)

## Exercise 05
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_person_order_order_date;
CREATE UNIQUE INDEX idx_person_order_order_date ON person_order(person_id, menu_id)
WHERE order_date = '2022-01-01';

EXPLAIN ANALYZE
SELECT person_id, menu_id FROM person_order
WHERE order_date = '2022-01-01';
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/7e43cc41-bb89-4a4b-9649-5ac758ece7a3)
![image](https://github.com/b0ryakha/SQL/assets/47691726/87da4aed-ef89-4a33-a43e-7833dca1a85d)

## Exercise 06
```sql
SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_1;
CREATE INDEX idx_1 ON pizzeria(id, rating);

EXPLAIN ANALYZE
SELECT
    m.pizza_name AS pizza_name,
    max(rating) OVER (PARTITION BY rating ORDER BY rating ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS k
FROM menu m
INNER JOIN pizzeria pz ON m.pizzeria_id = pz.id
ORDER BY 1, 2;
```
### Before:
![image](https://github.com/b0ryakha/SQL/assets/47691726/46c17088-6508-4e1a-8b1d-a61128c9beaf)

### After:
![image](https://github.com/b0ryakha/SQL/assets/47691726/031e2df9-18a9-41e9-bfc3-660ac8ad070f)
