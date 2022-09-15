15092022 1527
Tags: #z #dev

---
# Ограничения внешнего ключа

Позволяет задать столбец со значениями, которые будут ссылаться на строки в другой таблице. Обычно эти значения ссылаются на первичные ключи в другой таблице.

Внешний ключ может ссылаться на группу столбцов.

На внешний ключ можно задать ограничения, которые позволяют определить поведение при удалении связанных объектов.

## Пример

Определяем таблицы продуктов, заказов и таблицу для связки многие-ко-многим. Один продукт может быть во множестве заказов, один заказ может иметь множество продуктов.

Накладываем ограничения:
- при удалении продукта, если есть заказ с ним, то запрещаем удаление продукта
- при удалении заказа удаляем все записи из таблицы для связи многие-ко-многим

```sql
CREATE TABLE product (
    product_no integer PRIMARY KEY,
    name text,
);
CREATE TABLE order (
    order_id integer PRIMARY KEY,
    address text NOT NULL,
);
CREATE TABLE order_product (
    product_no integer REFERENCES product ON DELETE RESTRICT,
    order_id integer REFERENCES order_product ON DELETE CASCADE,
    quantity integer,
    PRIMARY KEY (product_no, order_id)
);
```

---
### Zero-Links
- 

---
### Links
- [[Ограничения (pgsql)]]