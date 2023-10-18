## 1)
```sql
SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
WHERE o.order_date BETWEEN '2023-07-17' AND '2023-10-17';
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/e9696dc3-5a07-4db7-ae5e-be0ee1ab53c2)

## 2)
```sql
SELECT p.category, FLOOR(AVG(o.quantity)) AS "average order size" FROM orders o
JOIN products p ON p.product_id = o.product_id
WHERE p.price >= 50
GROUP BY p.category, o.quantity;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/23b5ddcc-4846-46a6-921a-7754f4d37696)

## 3)
```sql
SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE SUM(p.price) > (SELECT AVG(p.price) FROM products p);
```

## 4)
```sql
WITH tmp_shit AS (
	SELECT p.product_id, SUM(p.price) AS "price_sum" FROM products p
	GROUP BY p.product_id, p.price
),
global_avg_price AS (
	SELECT AVG(p.price) FROM products p
)

SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN tmp_shit t ON t.product_id = o.product_id
WHERE t.price_sum > (SELECT * FROM global_avg_price);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/39f798bd-3812-4641-ad89-ca7d8833c05d)

## 5)
```sql

```

## 6)
```sql

```

## 7)
```sql

```

## 8)
```sql

```

## 9)
```sql

```

## 10)
```sql

```
