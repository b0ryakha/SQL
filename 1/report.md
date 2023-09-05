![База данных](/1/0.png)

## 1) SELECT ALL
```sql
SELECT * FROM Продукты;
```
![Результат](/1/1.png)

## 2) SELECT column
```sql
SELECT Продукты.Название FROM Продукты;
```
![Результат](/1/2.png)

## 3) SELECT SORT
```sql
SELECT Продукты.Название, Продукты.Цена FROM Продукты ORDER BY Продукты.Цена;
```
![Результат](/1/3.png)

## 4) SELECT GROUP
```sql
SELECT Название FROM Продукты GROUP BY Название;
```
![Результат](/1/4.png)

## 5) SELECT (вложенный)
