15092022 1417
Tags: #z #dev

---
# Ограничение NOT NULL и NULL

Ограничение NOT NULL эквивалентно ограничению CHECK(*столбец* IS NOT NULL). Лучше использовать просто NOT NULL, т.к. оно работает быстрее, но данному ограничению нельзя задать имя.

## Пример

Несколько ограничений на столбец

```sql
CREATE TABLE product (
    product_no integer,
    price numeric NOT NULL, CHECK(price > 0)
);
```

>[!note] NULL
> Ограничение NULL говорит о том, что значения столбца могут быть NULL
>```sql
>CREATE TABLE product (
>   product_no integer,
>   name text NULL
>);
>```

---
### Zero-Links
- 

---
### Links
- [[Ограничения (pgsql)]]