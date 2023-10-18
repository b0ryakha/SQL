## 1)
```sql
SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
GROUP BY c.customer_id, o.order_date
HAVING COUNT(c.customer_id) >= 2 AND o.order_date BETWEEN '2023-07-17' AND '2023-10-17';
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/fefa7db3-ac9c-499b-8eaa-21c1b0e8000a)

## 2)
```sql
SELECT p.category, FLOOR(AVG(o.quantity)) AS "average order size" FROM orders o
JOIN products p ON p.product_id = o.product_id
WHERE p.price >= 50
GROUP BY p.category;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/62fb14ff-5b9b-4d68-9b30-87196fec5c2c)

## 3)
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

## 4)
```sql
SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE p.price > 1000 AND p.category != 'Electronics';
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/22761f1c-9a3f-49cf-8c1b-2e680a12ebc8)

## 5)
```sql
DROP VIEW IF EXISTS v_customers_avg_price;
CREATE VIEW v_customers_avg_price AS (
	WITH customer_avg_price AS (
		SELECT o.customer_id, (SUM(p.price) / o.quantity) AS "avg_price" FROM orders o
		JOIN products p ON p.product_id = o.product_id
		GROUP BY o.customer_id, o.quantity
	),
	global_avg_price AS (
		SELECT AVG(p.price) FROM products p
	)
	
	SELECT c.first_name, c.last_name, c.email, cap.avg_price, (cap.avg_price - (SELECT * FROM global_avg_price)) AS "deviation" FROM customers c
	JOIN customer_avg_price cap ON cap.customer_id = c.customer_id
	GROUP BY c.first_name, c.last_name, c.email, cap.avg_price
);

SELECT * FROM v_customers_avg_price;
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
