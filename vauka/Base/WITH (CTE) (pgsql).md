23092022 1300
Tags: #z #dev

---
# Запросы WITH

*WITH* предоставляет способ записывать дополнительные операторы для применения в больших запросов. Таким образом, можно разбить большой запрос на несколько маленьких.

В *WITH* можно использовать следующие операторы:
- SELECT
- INSERT
- UPDATE
- DELETE

Использование *SELECT* дает возможность разбить большой запрос на несколько. Выполняется пока данные из *SELECT* востребованы главным запросом.

```sql
WITH reg_sales AS (
    SELECT SUM(price) AS total_sales, region
    FROM orders
    GROUP BY region
)
SELECT MAX(total_sales)
FROM reg_sales
WHERE region = 'MO';
```

```sql
-- рекурсивный запрос
WITH RECURSIVE t(n) AS (
    SELECT 1
    UNION ALL
    SELECT n + 1
    FROM t 
    WHERE n < 100
)
SELECT n FROM t;
```

Операторы в *WITH*, изменяющие данные, выполняются один раз и до конца. Эти операторы выполняются одновременно друг с другом и с основным запросом. Работают с одним снимком данных, не видят, как другие операторы меняют данные. Единственная возможность увидеть изменения - *RETURNING*.

```sql
WITH deleted AS (
    DELETE
    FROM orders
    WHERE price = 0
    RETURNING *
)
INSERT INTO orders_log VALUES SELECT * FROM deleted;
```

---
### Zero-Links
- [[00 PostgreSQL]]

---
### Links
- 