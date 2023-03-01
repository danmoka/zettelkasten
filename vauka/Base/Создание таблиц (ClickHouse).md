08112022 1550
Tags: #z #dev

---
# Создание БД, таблицы, заполнение данными

## Создание БД

После запуска контейнера с сервером CH и настроенным доступом подключаемся по адресу localhost:8123/play.

Команда

```SQL
CREATE DATABASE my_db;
```

## Создание таблицы

Создаем индекс на поле типа, а также сортируем (кажется тоже появляется индекс) на поле временной отметки.

Команда

```SQL
CREATE TABLE my_db.my_tb
(
    timestamp DateTime,
    type String,
	INDEX type_ind type TYPE bloom_filter GRANULARITY 8192
)
ENGINE = MergeTree()
ORDER BY timestamp
SETTINGS index_granularity = 8192
```

## Заполнение данными

Команда

```SQL
INSERT INTO TABLE cctv_click_db.cctv_click_tb
(
    `timestamp`,
    `type`
)
SELECT *
FROM (
    WITH
        'type_1' AS `type`,
        toDateTime('2022-09-19 10:00:40') AS `start`,
        toDateTime('2022-09-19 12:13:00') AS `end`
    SELECT arrayJoin(arrayMap(x -> toDateTime(x), range(toUInt32(`start`), toUInt32(`end`), 20))) AS `timestamp`, `brick_id`
);
```

---
### Zero-Links
- [[00 ClickHouse]]

---
### Links
- 