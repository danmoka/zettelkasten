16092022 1341
Tags: #z #dev

---
# Добавление данных в таблицу

Для добавления данных используется команда *INSERT* с указанием таблицы и значений строки, которую надо добавить в таблицу.

Если не все значения строки указаны, то берутся значения по умолчанию.
Если явно не указано какие столбцы заполняются значениями, то значения устанавливаются по порядку слева направо, остальное - дефолтными значениями.

## Пример

```sql
INSERT INTO product VALUES
    (1, 'Cheese', 99.0);

INSERT INTO product VALUES
    (2, 'Tomato', 9.0),
    (3, 'Potato', 5.5);

INSERT INTO product (product_no, name, price) VALUES
    (4, 'Chocolate', 10.0);

INSERT INTO products (name, price, product_no) VALUES
    ('Cheese', 9.99, 1);

INSERT INTO product VALUES
    SELECT product_no, name, price
    FROM new_products
    WHERE release_date = 'today'
```

---
### Zero-Links
- 

---
### Links
- [[Модификация данных (pgsql)]]