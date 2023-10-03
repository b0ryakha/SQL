## 1.1
```sql
SELECT * FROM Продукты;
```
Обычная выборка всех данных из таблицы.

## 1.3
```sql
SELECT Продукты.Название, Продукты.Цена FROM Продукты ORDER BY Продукты.Цена;
```
Выборка всех данных из таблицы, отсортированных по признаку.

---

## 2.1
```sql
INSERT INTO "Categories"(Title")
VALUES ('Техника'), ('Мебель'), ('Продукты'), ('Одежда'), ('Подарки')
```
Создание таблицы.

---

## 3.2
```sql
SELECT ("name", "age", "address") FROM "person" WHERE "address" = 'Moscow'
```
Выборка данных с условием.

## 3.5
```sql
SELECT "id" FROM "person_visits" WHERE "visit_date" BETWEEN '2022-01-01' and '2022-01-06' OR "pizzeria_id" = 2 ORDER BY "id"
```
Выборка данных с условным оператором BETWEEN, выбор данного оператора основан на простоте использования.

## 3.6
```sql
SELECT "name" FROM "person" WHERE (SELECT "id" FROM "person_order" WHERE "menu_id" = 3) = "id"
```
Выборка данных с вложенным запросом, вложенный запрос необходим для проверки условия.

## 3.7
```sql
SELECT EXISTS (SELECT "id" FROM "person" WHERE "name" = 'Kate')
```
Запрос, возвращающий true/false, в зависимости от данных.
Использовался функцию EXISTS, т.к. она выражает суть запроса.

---

## 4.1
```sql
SELECT "id", "pizza_name" FROM "menu"
UNION
SELECT "id", "name" FROM "person" ORDER BY "id", "pizza_name"
```
Запрос с объединением данных, использовался UNION для простоты запроса.

## 4.4
```sql
SELECT ABS(
	(SELECT COUNT("person_id") FROM "person_order" WHERE "order_date" = '2022-01-07')
	-
	(SELECT COUNT("person_id") FROM "person_visits" WHERE "visit_date" = '2022-01-07')
)
```
Запрос, который находит разницу между кол-вом записей.
Использовался функцию ABS, для корректного результата.

---

## 5.2
```sql
SELECT person_visits.visit_date AS action_date, person.name FROM person_visits, person
WHERE person_visits.visit_date IN (SELECT order_date FROM person_order)
```
В данном запросе использовалась связка операторов IN и SELECT по не опотности и для упрощения кода простого запроса.

## 5.3
```sql
SELECT order_date, (person.name || ' (age: ' || person.age || ')') AS person_info FROM person_order
JOIN person ON person_order.person_id = person.id
ORDER BY order_date, person_info
```
Выборка с использованием объединения и упорядочивания данных.
Используется оператор JOIN для оптимизации.

## 5.4
```sql
SELECT order_date, (person.name || ' (age: ' || person.age || ')') AS person_info FROM person_order
NATURAL JOIN person ORDER BY order_date, person_info
```
Выборка данных с объединением строк для красивого вывода результата.
Используется оператор NATURAL JOIN для естественного соединения, выполняемое по столбцам с одинаковыми именами.

---

## 6.2
```sql
SELECT missing_date::date FROM generate_series ('2022-01-01'::timestamp, '2022-01-10', '1 day') AS missing_date
LEFT JOIN person_visits ON visit_date = missing_date
WHERE visit_date IS NULL;
```
Выборка данных с функцией generate_series для сгенерирования временного промежутка.
Используется оператор LEFT JOIN для извлечения всех записей из первой таблицы и сопоставления их с записями во второй таблице.
