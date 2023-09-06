## 1)
```sql
--INSERT INTO "Products"("Product_id", "Product_title", "Product_description", "Price", "Quantity")
--VALUES ('Кирпич', 'красный и крепкий', 20, 1250), (6, 'Тележка', '', 145, 10), (7, 'Коробка', 'Уютная', 4, 5);

--UPDATE "Products"
--SET "Product_id" = 8
--WHERE "Product_id" = 0;

--ALTER TABLE "Products" ADD COLUMN "Category_id" "serial";

INSERT INTO "Categories"(Title")
VALUES ('Техника'), ('Мебель'), ('Продукты'), ('Одежда'), ('Подарки')

SELECT * FROM "Categories" ORDER BY "Category_id" ASC;
SELECT * FROM "Products" ORDER BY "Product_id" ASC;
```
![результат1](/2/1.png)
![результат2](/2/1.png)
