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

## 2.1
```sql
INSERT INTO "Categories"(Title")
VALUES ('Техника'), ('Мебель'), ('Продукты'), ('Одежда'), ('Подарки')
```
Создание таблицы.

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
Использовался оператор EXISTS, т.к. он выражает суть запроса.

## 4.1
```sql
SELECT "id", "pizza_name" FROM "menu"
UNION
SELECT "id", "name" FROM "person" ORDER BY "id", "pizza_name"
```
Запрос с объединением данных, использовался UNION для простоты запроса.

