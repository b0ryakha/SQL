## 1)
```sql
SELECT pizzeria.name, pizzeria.rating FROM pizzeria
WHERE pizzeria.id NOT IN (SELECT pizzeria_id FROM person_visits);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/215bc9c1-90cc-41be-adc7-0cc82185d09d)

## 2)
```sql
SELECT missing_date::date FROM generate_series ('2022-01-01'::timestamp, '2022-01-10', '1 day') AS missing_date
LEFT JOIN person_visits ON visit_date = missing_date
WHERE visit_date IS NULL;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/8ec32c7c-f9c2-4b34-ac70-ed5db0a60ca3)

## 3)
```sql

```

## 4)
```sql

```

## 5)
```sql
SELECT menu.pizza_name, pizzeria.name AS pizzeria_name, menu.price FROM "menu"
JOIN "pizzeria" ON pizzeria.id = menu.pizzeria_id
WHERE "pizza_name" = 'pepperoni pizza' OR "pizza_name" = 'mushroom pizza'
ORDER BY "pizza_name", "pizzeria_name";
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/adda8571-72c7-44de-a02e-96eda854220e)
