## Приложение: Спорт - жизнь
> Помогает отслеживать свои нагрузки, придумать упражнения.

---

## Схема баз данных
![image](https://github.com/b0ryakha/SQL/assets/47691726/52154a3c-06b7-4ab5-9b42-2d341503fe8d)

## Базы данных
### Продукт
#### Создание
```sql
CREATE TABLE product (
	id bigint PRIMARY KEY,
	title varchar,
	protein integer,
	carbohydrate integer,
	fats integer
);
```
#### Заполнение
```sql
INSERT INTO product VALUES (1, 'Pizza', 14, 36, 25);
INSERT INTO product VALUES (2, 'Pineapple', 4, 36, 25);
INSERT INTO product VALUES (3, 'Watermelon', 2, 15, 3);
INSERT INTO product VALUES (4, 'Soda', 6, 16, 25);
INSERT INTO product VALUES (5, 'Avocado', 3, 25, 4);
INSERT INTO product VALUES (6, 'Apple', 5, 31, 9);
```

### Рацион
#### Создание
```sql
CREATE TABLE diet (
	id bigint PRIMARY KEY,
	product_id bigint,
	eat_date date NOT NULL,
	
	CONSTRAINT fk_product_product_id FOREIGN KEY (product_id) REFERENCES product(id)
);
```
#### Заполнение
```sql
INSERT INTO diet VALUES (1, 1, '2023-12-14');
INSERT INTO diet VALUES (2, 2, '2023-01-28');
INSERT INTO diet VALUES (3, 2, '2022-05-28');
```
#### View
```sql
DROP VIEW IF EXISTS v_diet_product;
CREATE VIEW v_diet_product AS (
	SELECT d.id AS "diet id", p.title
	FROM diet d
	JOIN product p ON d.product_id = p.id
);
```

### Роль
#### Создание
```sql
CREATE TABLE role (
	id integer PRIMARY KEY,
	title varchar DEFAULT 'client' CHECK(title IN ('coach', 'client'))
);
```
#### Заполнение
```sql
INSERT INTO role VALUES (1, 'client');
INSERT INTO role VALUES (2, 'coach');
```

### Цель
#### Создание
```sql
CREATE TABLE purposes (
	id bigint PRIMARY KEY,
	title varchar NOT NULL,
	description varchar,
	is_completed boolean
);
```
#### Заполнение
```sql
INSERT INTO purposes VALUES (1, 'Eat food', 'Just eat random food.', false);
INSERT INTO purposes VALUES (2, 'Water is pure', 'Drink taste water', false);
INSERT INTO purposes VALUES (3, 'Lose weight', 'Exercise and lose weight.', false);
```

### Пользователь
#### Создание
```sql
CREATE TABLE person (
	id bigint PRIMARY KEY,
	name varchar NOT NULL,
	age integer NOT NULL,
	gender varchar DEFAULT 'female' CHECK(gender IN ('female', 'male')),
	phone varchar,
	role_id integer DEFAULT 1 NOT NULL,
	diet_id integer,
	purposes_id bigint,

	CONSTRAINT fk_role_role_id FOREIGN KEY (role_id) REFERENCES role(id),
	CONSTRAINT fk_diet_diet_id FOREIGN KEY (diet_id) REFERENCES diet(id),
	CONSTRAINT fk_purposes_purposes_id FOREIGN KEY (purposes_id) REFERENCES purposes(id)
);

CREATE TABLE diet_person (
	diet_id bigint NOT NULL,
	person_id bigint NOT NULL,

	CONSTRAINT fk_diet_diet_id FOREIGN KEY (diet_id) REFERENCES diet(id),
	CONSTRAINT fk_person_person_id FOREIGN KEY (person_id) REFERENCES person(id)
);

CREATE TABLE purposes_person (
	purposes_id bigint NOT NULL,
	person_id bigint NOT NULL,

	CONSTRAINT fk_purposes_purposes_id FOREIGN KEY (purposes_id) REFERENCES purposes(id),
	CONSTRAINT fk_person_person_id FOREIGN KEY (person_id) REFERENCES person(id)
);
```
#### Views
```sql
DROP VIEW IF EXISTS v_person_role;
CREATE VIEW v_person_role AS (
	SELECT r.title FROM "role" r
	JOIN person p ON p.role_id = r.id
);

DROP VIEW IF EXISTS v_person_result;
CREATE VIEW v_person_result AS (
	SELECT p.name, r.estimation FROM "person" p
	JOIN result r ON p.id = r.person_id
);
```

#### Заполнение
```sql
INSERT INTO person VALUES (1, 'Anna', 16, 'female', '89423386477', 2, 1, 1);
INSERT INTO person VALUES (2, 'Artem', 16, 'male', '89424564477', 2, 2, 1);
INSERT INTO person VALUES (3, 'Anton', 16, 'male', '84457806477', 1, 2, 2);
INSERT INTO person VALUES (4, 'Leha', 16, 'male', '83421526294', 1, 3, 2);
INSERT INTO person VALUES (5, 'Petya', 16, 'male', '89364243751', 1, 1, 1);
INSERT INTO person VALUES (6, 'Leva', 16, 'male', '89642585845', 1, 3, 1);
INSERT INTO person VALUES (7, 'Anastasia', 16, 'female', '89372458485', 1, 1, 3);
INSERT INTO person VALUES (8, 'Karalina', 16, 'female', '89624528523', 1, 2, 3);

INSERT INTO diet_person VALUES (1, 1);
INSERT INTO diet_person VALUES (1, 2);
INSERT INTO diet_person VALUES (1, 3);
INSERT INTO diet_person VALUES (1, 4);
INSERT INTO diet_person VALUES (1, 5);
INSERT INTO diet_person VALUES (1, 6);
INSERT INTO diet_person VALUES (1, 7);
INSERT INTO diet_person VALUES (1, 8);
INSERT INTO diet_person VALUES (2, 1);
INSERT INTO diet_person VALUES (2, 2);
INSERT INTO diet_person VALUES (2, 3);
INSERT INTO diet_person VALUES (2, 4);
INSERT INTO diet_person VALUES (2, 5);
INSERT INTO diet_person VALUES (2, 6);
INSERT INTO diet_person VALUES (2, 7);
INSERT INTO diet_person VALUES (2, 8);
INSERT INTO diet_person VALUES (3, 1);
INSERT INTO diet_person VALUES (3, 2);
INSERT INTO diet_person VALUES (3, 3);
INSERT INTO diet_person VALUES (3, 4);
INSERT INTO diet_person VALUES (3, 5);
INSERT INTO diet_person VALUES (3, 6);
INSERT INTO diet_person VALUES (3, 7);
INSERT INTO diet_person VALUES (3, 8);

INSERT INTO purposes_person VALUES (1, 1);
INSERT INTO purposes_person VALUES (1, 2);
INSERT INTO purposes_person VALUES (1, 3);
INSERT INTO purposes_person VALUES (1, 4);
INSERT INTO purposes_person VALUES (1, 5);
INSERT INTO purposes_person VALUES (1, 6);
INSERT INTO purposes_person VALUES (1, 7);
INSERT INTO purposes_person VALUES (1, 8);
INSERT INTO purposes_person VALUES (2, 1);
INSERT INTO purposes_person VALUES (2, 2);
INSERT INTO purposes_person VALUES (2, 3);
INSERT INTO purposes_person VALUES (2, 4);
INSERT INTO purposes_person VALUES (2, 5);
INSERT INTO purposes_person VALUES (2, 6);
INSERT INTO purposes_person VALUES (2, 7);
INSERT INTO purposes_person VALUES (2, 8);
INSERT INTO purposes_person VALUES (3, 1);
INSERT INTO purposes_person VALUES (3, 2);
INSERT INTO purposes_person VALUES (3, 3);
INSERT INTO purposes_person VALUES (3, 4);
INSERT INTO purposes_person VALUES (3, 5);
INSERT INTO purposes_person VALUES (3, 6);
INSERT INTO purposes_person VALUES (3, 7);
INSERT INTO purposes_person VALUES (3, 8);
```

### Группа
#### Создание
```sql
CREATE TABLE _group (
	id bigint PRIMARY KEY,
	group_id integer NOT NULL,
	coach_id bigint NOT NULL,
	client_id bigint NOT NULL,
	
	CONSTRAINT fk_person_coach_id FOREIGN KEY (coach_id) REFERENCES person(id),
	CONSTRAINT fk_person_client_id FOREIGN KEY (client_id) REFERENCES person(id)
);
```
#### Заполнение
```sql
INSERT INTO _group VALUES (1, 1, 1, 3);
INSERT INTO _group VALUES (2, 1, 1, 4);
INSERT INTO _group VALUES (3, 1, 1, 5);
INSERT INTO _group VALUES (4, 2, 2, 6);
INSERT INTO _group VALUES (5, 2, 2, 7);
INSERT INTO _group VALUES (6, 2, 2, 8);
```

### Результат
#### Создание
```sql
CREATE TABLE result (
	id bigint PRIMARY KEY,
	person_id bigint NOT NULL,
	completion_date date NOT NULL,
	estimation integer NOT NULL CHECK(estimation >= 0 AND estimation <= 10),
	
	CONSTRAINT fk_person_person_id FOREIGN KEY (person_id) REFERENCES person(id)
);
```
#### Заполнение
```sql
INSERT INTO result VALUES (1, 3, '2022-12-25', 6);
INSERT INTO result VALUES (2, 4, '2023-08-25', 10);
INSERT INTO result VALUES (3, 5, '2023-02-25', 1);
INSERT INTO result VALUES (4, 6, '2022-03-25', 5);
INSERT INTO result VALUES (5, 7, '2022-05-25', 7);
INSERT INTO result VALUES (6, 8, '2022-11-25', 6);
```

#### Триггеры
```sql
CREATE OR REPLACE FUNCTION fnc_after_new_couch_inserts() RETURNS trigger AS $trg_after_new_couch_insert$
BEGIN
INSERT INTO couchs(person_id)
SELECT NEW.id;
WHERE NEW.role_id = 'couch'
RETURN NULL;
END;
$trg_after_new_couch_insert$ LANGUAGE 'plpgsql';

CREATE TRIGGER trg_after_new_couch_insert AFTER INSERT ON person
	FOR EACH ROW EXECUTE FUNCTION fnc_after_new_couch_inserts();
```
```sql
CREATE OR REPLACE FUNCTION fnc_after_insert_in_highest_grade() RETURNS TRIGGER AS $trg_after_insert_in_highest_grade$
BEGIN
UPDATE result r
JOIN person p ON p.id = r.person_id
WHERE r.estimation = 10;
RETURN NULL;
END;
$trg_after_insert_in_highest_grade$ LANGUAGE 'plpgsql';

CREATE TRIGGER trg_after_highest_grade_insert AFTER INSERT ON highest_grade
	FOR EACH ROW EXECUTE FUNCTION fnc_after_insert_in_highest_grade_inserts()
```
