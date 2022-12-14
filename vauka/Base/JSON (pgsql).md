19092022 1627
Tags: #z #dev

---
# Тип данных JSON

PostgreSQL позволяет хранить данные в формате JSON. Такие данные можно было бы хранить и в типе text, но в таком случае отсутствуют проверки на корректность формата JSON.

Для хранения данных в формате JSON в PostgreSQL есть два типа: json и jsonb. Тип jsonb разбирает, переданные ему данные в формате json. jsonb не сохраняет порядок ключей, удаляет незначащие пробелы, дает возможность навесить индексы, и преобразует тип данных во внутренние.

Хранимые данные в формате json должны быть максимально атомарными (нельзя разделить меньше), т.к. при изменении данных идет блокировка всей строки (как обычно), и если json большой, то строка будет дольше заблокирована.

Для jsonb также существуют проверки на вхождение (входит ли объект справа в объект слева) и существования.

```sql
-- Порядок элементов в массиве не важен, поэтому это условие тоже выполняется:
SELECT '[1, 2, 3]'::jsonb @> '[3, 1]'::jsonb;
-- Строка существует в качестве ключа объекта:
SELECT '{"foo": "bar"}'::jsonb ? 'foo';
```

## Синтаксис вводимых и выводимых значений

jsonb будет выводить числовые данные, приведенный к типу numeric в PostgreSQL (а json - нет). Числа, заданные в записи с Е будут преобразованы в запись без Е.

```sql
SELECT '{"bar": 12, "foo": [1.230e-5, "tag", null] }'::jsonb
-- {"bar": 12, "foo": [0.00001230, "tag", null]}
```

---
### Zero-Links
- [[00 PostgreSQL]]

---
### Links
- 