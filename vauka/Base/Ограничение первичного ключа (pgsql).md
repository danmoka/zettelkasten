15092022 1509
Tags: #z #dev

---
# Ограничения первичного ключа

Позволяет задать ограничение, по которому можно определять уникальность каждой строки в таблице. Может состоять из нескольких столбцов.

Грубо говоря, PRIMARY KEY =  UNIQUE NOT NULL

## Пример

```sql
CREATE TABLE product (
    product_no integer PRIMARY KEY,
    price numeric,
    name text
);
```

---
### Zero-Links
- 

---
### Links
- [[Ограничения (pgsql)]]