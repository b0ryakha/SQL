## 1)
```sql
insert into person values (10, 'Katya', 2, 'female', 'Kazan');
insert into person values (11, 'Andrey', 15, 'male', 'Kazan');
insert into person values (12, 'Kate', 13, 'female', 'Novosibirsk');
insert into person values (13, 'Denis', 12, 'male', 'Kazan');
insert into person values (14, 'Elvira', 45, 'female', 'Kazan');
insert into person values (15, 'Irina', 20, 'female', 'Saint-Petersburg');

insert into pizzeria values (7,'Pizza Hut v2', 4.6);
insert into pizzeria values (8,'Dominos', 3.3);
insert into pizzeria values (9,'juju Pizza', 1.2);
insert into pizzeria values (10,'mama Johns', 4.9);
insert into pizzeria values (11,'good Pizza', 5);
insert into pizzeria values (12,'DinoPizza', 4.2);

insert into person_visits values (20, 4, 1, '2022-01-01');
insert into person_visits values (21, 2, 2, '2022-01-01');
insert into person_visits values (22, 5, 1, '2022-01-02');
insert into person_visits values (23, 3, 5, '2022-01-03');
insert into person_visits values (24, 3, 6, '2022-02-04');
insert into person_visits values (25, 4, 5, '2022-02-07');
insert into person_visits values (26, 4, 6, '2022-02-08');
insert into person_visits values (27, 5, 2, '2022-02-08');
insert into person_visits values (28, 5, 6, '2022-02-09');
insert into person_visits values (29, 6, 2, '2022-02-09');
insert into person_visits values (30, 6, 4, '2000-01-01');
insert into person_visits values (31, 6, 1, '2022-01-03');
insert into person_visits values (32, 6, 2, '2022-01-05');
insert into person_visits values (33, 8, 1, '2022-01-09');
insert into person_visits values (34, 8, 2, '2022-01-11');
insert into person_visits values (35, 8, 4, '2022-01-07');
insert into person_visits values (36, 9, 4, '2022-01-08');
insert into person_visits values (37, 9, 5, '2022-01-09');
insert into person_visits values (38, 9, 6, '2022-01-10');

insert into menu values (19,5,'italio pizza', 41);
insert into menu values (20,5,'dodo pizza', 212);
insert into menu values (21,5,'nike pizza', 112);
insert into menu values (22,5,'cake pizza', 452);
insert into menu values (23,5,'diamond pizza', 25);
insert into menu values (24,5,'228 pizza', 424);

insert into person_order values (11,5, 16, '2018-01-07');
insert into person_order values (12,3, 17, '2000-01-07');
insert into person_order values (13,6, 18, '2022-09-07');
insert into person_order values (14,6, 6, '2022-09-08');
insert into person_order values (15,1, 7, '2022-09-08');

```
![результат1](/3/1.png)
![результат2](/3/2.png)
![результат2](/3/3.png)
![результат2](/3/4.png)
![результат2](/3/5.png)

## 2)
```sql
SELECT ("name", "age", "address") FROM "person" WHERE "address" = 'Moscow'
```
![результат1](/3/6.png)

## 3)
```sql
SELECT ("name", "age", "address") FROM "person" WHERE "gender" = 'female' and "address" = 'Moscow' ORDER BY "name"
```
![результат1](/3/7.png)
