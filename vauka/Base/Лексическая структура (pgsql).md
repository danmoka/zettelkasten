15092022 1028
Tags: #z #dev

---
# Лексическая структура программ SQL

*Программа* SQL состоит из последовательности *команд*.
Команда заканчивается символом **;** или окончанием входного потока.
Каждая команда состоит из *компонентов*:
- идентификаторы
- идентификаторы в кавычках
- константы и спец символы
- ключевые слова

## Пример

Три команды с ключевыми словами и символом **;**
Например, *UPDATE* и *SET* - ключевые слова для команды обновления.

```sql
SELECT * FROM MY_TABLE;
UPDATE MY_TABLE SET A = 5;
INSERT INTO MY_TABLE VALUES (3, 'Hello World!');
```

---
### Zero-Links
- [[00 PostgreSQL]]

---
### Links
- 
---
### Outer links
- https://postgrespro.ru/docs/postgresql/9.6/sql-syntax-lexical#sql-syntax-constants
