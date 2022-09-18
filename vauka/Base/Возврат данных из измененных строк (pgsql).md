17092022 1252
Tags: #z #dev

---
# Возврат данных

Для команд *INSERT, UPDATE, DELETE* можно использовать ключевое слово *RETURNING*, которое позволяет без дополнительного запроса возвращать информацию об измененных строках.

## INSERT

При вставке данных удобно отслеживать сгенерированный id строки.

```sql
INSERT INTO product (price, name)
VALUES
    (10.0, 'potato')
RETURNING id;
```

## UPDATE

При обновлении можно узнать новые значения обновленных строк

```sql
UPDATE product
SET price = price + 5.0
RETURNING price as new_price;
```

## DELETE

При удалении отследить то, какие строки были удалены

```sql
DELETE
FROM product
WHERE id = 10
RETURNING *;
```

---
### Zero-Links
- 

---
### Links
- [[Удаление данных (pgsql)]]
- [[Изменение данных (pgsql)]]
- [[Добавление данных (pgsql)]]