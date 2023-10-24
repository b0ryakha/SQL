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
DROP VIEW IF EXISTS v_avg_order;
CREATE VIEW v_avg_order AS (
	WITH sum_order_id AS (
		SELECT o.order_id, o.customer_id, o.quantity, SUM(p.price) AS "sum" FROM orders o
		JOIN products p ON p.product_id = o.product_id
		GROUP BY o.order_id
	),
	avg_sum_customer AS (
		SELECT s.customer_id, AVG(s.sum) AS "avg_sum" FROM sum_order_id s
		GROUP BY s.customer_id
	),
	avg_all_sum AS (
		SELECT AVG(s.sum) AS "avg_all" FROM sum_order_id s
	)
	
	SELECT c.first_name, c.last_name, ROUND(a.avg_sum, 2), ROUND(a.avg_sum - (SELECT avg_all FROM avg_all_sum), 2) AS difference FROM avg_sum_customer a
	JOIN customers c ON c.customer_id = a.customer_id
	JOIN sum_order_id s ON s.customer_id = a.customer_id
	GROUP BY c.first_name, c.last_name, a.avg_sum
);

SELECT * FROM v_avg_order
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/9a1b10ea-4ebc-4163-a722-a511ede60a76)

## 6)
```sql
WITH tmp AS (
	SELECT * FROM (
		SELECT o.customer_id, o.order_date, row_number() OVER(PARTITION BY o.customer_id ORDER BY o.order_date DESC) AS order_id
		FROM orders o
	) tmp WHERE order_id < 3
),
improved_order_dates AS (
	SELECT DISTINCT
		t.customer_id,
		(
			SELECT order_date FROM tmp WHERE order_id = 1 AND customer_id = t.customer_id
		) AS "order_date1",
		(
			SELECT order_date FROM tmp WHERE order_id = 2 AND customer_id = t.customer_id
		) AS "order_date2"
	FROM
		tmp t
),
customer_period AS (
	SELECT customer_id, ABS(order_date1 - order_date2) AS "day_period" FROM improved_order_dates
)

SELECT cs.customer_id, cs.first_name, cs.last_name, cs.email, cs.address FROM customer_period cp
JOIN customers cs ON cs.customer_id = cp.customer_id
WHERE cp.day_period = (SELECT MAX(day_period) FROM customer_period)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/6e8e7bd6-cc27-4603-abac-5ee9940fad27)

## 7)
```sql
SELECT c.customer_id, c.first_name, c.last_name, c.email, c.address FROM customers c
LEFT JOIN orders o ON o.customer_id = c.customer_id
WHERE o.order_date BETWEEN '2023-08-24' AND '2023-10-24'
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/c31d1630-476c-48a5-92b4-c57764ecb9f9)

## 8)
```sql
UPDATE products
SET price = price - ((price * 10) / 100)
WHERE category = 'Clothing'
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/ddda76e5-989d-4efe-be30-5d0dc4dfd930)

## 9)
```sql
WITH category_avg_price AS (
	SELECT category AS "category_name", AVG(price) AS "avg_price" FROM products
	GROUP BY category
)

SELECT
	category_name AS "category with max avg price",
	(
		SELECT category_name FROM category_avg_price
	    WHERE avg_price = (SELECT MIN(avg_price) FROM category_avg_price)
	) AS "category with min avg price"
FROM
	category_avg_price
WHERE
	avg_price = (SELECT MAX(avg_price) FROM category_avg_price);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/ab7c1305-09bc-41df-8378-60fdc8d2beb7)

## 10)
```sql
DELETE FROM orders o1
WHERE o1.quantity > (SELECT AVG(o2.quantity) FROM orders o2);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/0323a986-ed0d-4ac1-81aa-32b4a268928d)
