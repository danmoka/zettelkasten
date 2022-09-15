15092022 1225
Tags: #z #dev

---
# Позиционная передача аргументов

Позиционные аргументы можно передавать в любом порядке. Параметры со значениями по умолчанию можно пропускать.

## Пример

Функция

```sql
CREATE FUNCTION concat_lower_or_upper(a text, b text, uppercase boolean DEFAULT false)
RETURNS text
AS
$$
SELECT CASE
    WHEN $3 THEN UPPER($1 || ' ' || $2)
    ELSE LOWER($1 || ' ' || $2)
    END;
$$
```

Вызов

```sql
SELECT concat_lower_or_upper('Hello', 'World')
SELECT concat_lower_or_upper('Hello', 'World', true)
```


---
### Zero-Links
- 

---
### Links
- [[Вызов функций (pgsql)]]