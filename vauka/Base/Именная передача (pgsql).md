15092022 1233
Tags: #z #dev

---
# Именная передача аргументов

Для передачи указывается имя параметра. Основное преимущество - возможность записывать аргументы в любом порядке.

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
SELECT concat_lower_or_upper(a => 'Hello', b => 'World')
SELECT concat_lower_or_upper(a => 'Hello', b => 'World', uppercase => true)
```

---
### Zero-Links
- [[00 PostgreSQL]]

---
### Links
- 