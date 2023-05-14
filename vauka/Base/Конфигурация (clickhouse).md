01032023 1635
Tags: #z #dev

---
# Конфигурация ClickHouse

Конфигурация ClickHouse состоит из двух частей: 
- *config.xml* - настройки сервера;
- *users.xml* - настройки пользователей.

По умолчанию конфигурация хранится в папке `etc/clickhouse-server/`
Рекомендуется помещать собственные настройки в отдельные **.xml** файлы в подпапках:
-   `/etc/clickhouse-server/users.d` — подпапка для **пользовательских настроек**;
-   `/etc/clickhouse-server/config.d` — подпапка для **настроек сервера**;
-   `/etc/clickhouse-server/conf.d` — подпапка для **любых (обоих) настроек**.

## Пример

Требуется увеличить максимальный размер строки, которая обрабатывается SQL парсером. Решение: добавить/изменить настройку с помощью файлов конфигурации в `config.d` <max_query_size><max_query_size>.

---
### Zero-Links
- [[00 ClickHouse]]
- [[00 Python]]

---
### Links
- 
---
### Outer links
- https://ivan-shamaev.ru/how-to-write-data-to-clickhouse-using-python/