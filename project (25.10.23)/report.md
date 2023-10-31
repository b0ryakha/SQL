## Приложение: Спорт - жизнь
### Помогает отслеживать свои нагрузки, придумать упражнения.

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

### Роль
#### Создание
```sql
CREATE TABLE role (
	id integer PRIMARY KEY,
	title varchar DEFAULT 'client' CHECK(title IN ('coach', 'client'))
);
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
