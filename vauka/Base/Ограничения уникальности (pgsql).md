15092022 1426
Tags: #z #dev

---
# Ограничения уникальности

Ограничение уникальности на столбец говорит о том, что значения столбца должны быть уникальными. Значения NULL могут считаться уникальными, поэтому значения столбца могут быть всё равно дублироваться.

Ограничение уникальности на несколько столбцов говорит о том, что сочетания значений столбцов должны быть уникальны, а значения самих столбцов могут дублироваться.

## Пример

```sql
CREATE TABLE product (
    product_no integer,
    price numeric NOT NULL, CHECK(price > 0),
    name text UNIQUE
);

CREATE TABLE product (
    product_no integer,
    price numeric NOT NULL, CHECK(price > 0),
    name text,
    group text,
    CONSTRAINT valid_name_group UNIQUE(name, group)
);
```

---
### Zero-Links
- first
- second

---
### Links
- first
- second