15092022 1359
Tags: #z #dev

---
# Ограничение-проверка на столбцы и таблицу

Ограничение-проверка представляет из себя выражение, которое принимает проверяемое значение и возвращает true, false или NULL.

Ограничение пройдено, если возвращается true или NULL.

## Пример

Ограничение на столбец

```sql
CREATE TABLE product (
    product_no integer,
    price numeric CHECK (price > 0),
    discounted_price numeric (discounted_price > 0),
);
```

Ограничение на таблицу

```sql
CREATE TABLE product (
    product_no integer,
    price numeric CHECK (price > 0),
    discounted_price numeric (discounted_price > 0),
    CHECK (price > discounted_price) 
    /* ^ ограничение на таблицу */
);

CREATE TABLE product (
    product_no integer,
    price numeric CHECK (price > 0),
    discounted_price numeric,
    CHECK (discounted_price > 0 AND price > discounted_price) 
    /* ^ ограничение на таблицу */
);
```

Также ограничению можно задать имя, что удобно при разборе ошибок

```sql
CREATE TABLE product (
    product_no integer,
    price numeric CHECK (price > 0),
    discounted_price numeric,
    CONSTRAINT valid_discount CHECK (discounted_price > 0 AND price > discounted_price) 
    /* ^ ограничение на таблицу с заданным именем*/
);
```

---
### Zero-Links
- 

---
### Links
- [[Ограничения (pgsql)]]