15092022 1237
Tags: #z #dev

---
# Смешанная передача аргументов

Главное правило: сначала позиционные, затем именованные. После именованных позиционных быть не может.

##  Пример

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
SELECT concat_lower_or_upper('Hello', b => 'World')
SELECT concat_lower_or_upper('Hello', b => 'World', uppercase => true)
```

---
### Zero-Links
- 

---
### Links
- [[Вызов функций (pgsql)]]