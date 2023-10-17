## Exercise 00
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint,
	pizzeria_id bigint,
	discount numeric,
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);
```

## Exercise 01
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint,
	pizzeria_id bigint,
	discount numeric,
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);

DROP VIEW IF EXISTS amount;
CREATE VIEW amount AS (
	WITH discount AS (
		SELECT person_id, pizzeria_id FROM person_order
		JOIN menu ON menu.id = person_order.menu_id
	)
	
	SELECT person_id, pizzeria_id, COUNT(*) AS orders_amount FROM discount   
	GROUP BY person_id, pizzeria_id ORDER BY 1
);

INSERT INTO person_discounts(id, person_id, pizzeria_id, discount)
SELECT ROW_NUMBER() OVER (ORDER BY 1), person_id, pizzeria_id, 
(CASE
	WHEN orders_amount = 1 THEN 10.5
	WHEN orders_amount = 2 THEN 22
	ELSE 30
END) AS discount
FROM amount;

SELECT * FROM person_discounts;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/6bc87507-ce66-4c43-bc47-e9ba9c58922d)

## Exercise 02
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint,
	pizzeria_id bigint,
	discount numeric,
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);

DROP VIEW IF EXISTS amount;
CREATE VIEW amount AS (
	WITH discount AS (
		SELECT person_id, pizzeria_id FROM person_order
		JOIN menu ON menu.id = person_order.menu_id
	)
	
	SELECT person_id, pizzeria_id, COUNT(*) AS orders_amount FROM discount   
	GROUP BY person_id, pizzeria_id ORDER BY 1
);

INSERT INTO person_discounts(id, person_id, pizzeria_id, discount)
SELECT ROW_NUMBER() OVER (ORDER BY 1), person_id, pizzeria_id, 
(CASE
	WHEN orders_amount = 1 THEN 10.5
	WHEN orders_amount = 2 THEN 22
	ELSE 30
END) AS discount
FROM amount;

SELECT p.name, m.pizza_name, m.price, ROUND(SUM(m.price - (m.price / 100) * pd.discount)) AS "discount_price", piz.name FROM person_discounts pd
JOIN person p ON p.id = pd.person_id
JOIN menu m ON m.pizzeria_id = pd.pizzeria_id
JOIN pizzeria piz ON piz.id = pd.pizzeria_id
GROUP BY p.name, m.pizza_name, m.price, piz.name;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/85b0521a-5772-46f2-9092-adec34f29c07)

## Exercise 03
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint,
	pizzeria_id bigint,
	discount numeric,
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);

DROP VIEW IF EXISTS amount;
CREATE VIEW amount AS (
	WITH discount AS (
		SELECT person_id, pizzeria_id FROM person_order
		JOIN menu ON menu.id = person_order.menu_id
	)
	
	SELECT person_id, pizzeria_id, COUNT(*) AS orders_amount FROM discount   
	GROUP BY person_id, pizzeria_id ORDER BY 1
);

INSERT INTO person_discounts(id, person_id, pizzeria_id, discount)
SELECT ROW_NUMBER() OVER (ORDER BY 1), person_id, pizzeria_id, 
(CASE
	WHEN orders_amount = 1 THEN 10.5
	WHEN orders_amount = 2 THEN 22
	ELSE 30
END) AS discount
FROM amount;

SET enable_seqscan = OFF;

DROP INDEX IF EXISTS idx_person_discounts_unique;
CREATE UNIQUE INDEX idx_person_discounts_unique ON person_discounts(person_id, pizzeria_id);

EXPLAIN ANALYZE
SELECT p.name, m.pizza_name, m.price, ROUND(SUM(m.price - (m.price / 100) * pd.discount)) AS "discount_price", piz.name FROM person_discounts pd
JOIN person p ON p.id = pd.person_id
JOIN menu m ON m.pizzeria_id = pd.pizzeria_id
JOIN pizzeria piz ON piz.id = pd.pizzeria_id
GROUP BY p.name, m.pizza_name, m.price, piz.name
ORDER BY p.name;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/00f811b6-65c9-4202-8798-e6fcee90fb5e)

## Exercise 04
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint NOT NULL,
	pizzeria_id bigint NOT NULL,
	discount numeric NOT NULL DEFAULT 0 CHECK (discount >=0 AND discount <= 100),
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);
```

## Exercise 05
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint NOT NULL,
	pizzeria_id bigint NOT NULL,
	discount numeric NOT NULL DEFAULT 0 CHECK (discount >= 0 AND discount <= 100),
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);

COMMENT ON TABLE person_discounts IS 'A table that stores the IDs of visitors and pizzerias, as well as their discounts';
```

## Exercise 06
```sql
DROP TABLE IF EXISTS person_discounts;
CREATE TABLE person_discounts (
	id bigint primary key,
	person_id bigint NOT NULL,
	pizzeria_id bigint NOT NULL,
	discount numeric NOT NULL DEFAULT 0 CHECK (discount >= 0 AND discount <= 100),
	
	constraint fk_person_discounts_person_id foreign key(person_id) references person(id),
	constraint fk_person_discounts_pizzeria_id foreign key(pizzeria_id) references pizzeria(id)
);

DROP SEQUENCE IF EXISTS seq_person_discounts;
CREATE SEQUENCE seq_person_discounts
MINVALUE 1 START WITH 1 INCREMENT BY 1;

ALTER TABLE person_discounts ALTER COLUMN id SET DEFAULT NEXTVAL('seq_person_discounts');
```
