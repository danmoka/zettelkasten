20092022 1703
Tags: #z #dev

---
# Оконные функции

Данные функции позволяют выполнять вычисления над набором строк.

## ROW_NUMBER

Данная функция нумерует строки по порядку, начиная с 1. Параметр *PARTITION BY* позволяет разбить набор на группы, внутри которых нумерация будет независима от других групп. *ORDER BY* задает сортировку строк.

```sql
SELECT *,
    ROW_NUMBER() OVER (
        PARTITION BY product.shop
        ORDER BY product.price
    )
FROM product;
-- 1 S1 potato 10
-- 2 S1 tomato 12
-- 1 S2 milk 5
-- 2 S2 chocolate 7
-- 3 S2 ...
```

## RANK

Представляет собой ранжирование строк. Строкам, у которых параметр одинаков, дается одинаковый ранг. Если несколько строк имеют одинаковый ранг, то следующие ранги пропускаются.

```sql
SELECT *,
    RANK() OVER (
        ORDER BY product.price
    )
FROM product;
-- 1 S1 potato 10
-- 1 S1 tomato 10
-- 3 S2 milk 12
-- 4 S2 chocolate 17
-- 4 S2 ... 17
```

## DENSE_RANK

Ранжирование без пропусков.

```sql
SELECT *,
    DENSE_RANK() OVER (
        ORDER BY product.price
    )
FROM product;
-- 1 S1 potato 10
-- 1 S1 tomato 10
-- 2 S2 milk 12
-- 3 S2 chocolate 17
-- 3 S2 ... 17
```

---
### Zero-Links
- 

---
### Links
- [[Функции и операторы (pgsql)]]