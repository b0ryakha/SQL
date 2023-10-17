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


```
