## Exercise 00
```sql
DROP VIEW IF EXISTS males, females;

CREATE VIEW males AS
	SELECT * FROM person WHERE gender = 'male';
	
CREATE VIEW females AS
	SELECT * FROM person WHERE gender = 'female';
	
SELECT * FROM males, females;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b6ca6df6-c9df-4e8f-b405-6d7582e39c4f)

## Exercise 01
```sql
DROP VIEW IF EXISTS v_males, v_females;

CREATE VIEW v_males AS
	SELECT * FROM person WHERE gender = 'male';
	
CREATE VIEW v_females AS
	SELECT * FROM person WHERE gender = 'female';

SELECT "name" FROM v_males
UNION
SELECT "name" FROM v_females
ORDER BY "name";
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b1d28390-9505-4395-9a74-d5b563b647ab)


## Exercise 02
```sql
DROP VIEW IF EXISTS v_generated_dates;

CREATE VIEW v_generated_dates AS
	SELECT generate_series('01.01.2022', '31.01.2022', interval '1 day')::date AS generated_date
	ORDER BY generated_date;

SELECT * FROM v_generated_dates;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/27385d3d-88b2-4e97-974f-0b9df8b919f8)


## Exercise 03
```sql
DROP VIEW IF EXISTS v_generated_dates;

CREATE VIEW v_generated_dates AS
	SELECT generate_series('01.01.2022', '31.01.2022', interval '1 day')::date AS generated_date
	ORDER BY generated_date;

SELECT generated_date FROM v_generated_dates
LEFT JOIN person_visits ON generated_date = visit_date
WHERE visit_date IS NULL;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/dfdc07db-8d52-466f-b13b-4eb595fb0ba0)

## Exercise 04
```sql

```
