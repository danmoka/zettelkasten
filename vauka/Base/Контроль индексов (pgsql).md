21092022 1433
Tags: #z #dev

---
# Контроль использования индексов

Вообще, индексы, в основном, не нуждаются в обслуживании, но иногда полезно узнать, как и какие индексы используются при помощи команды *EXPLAIN*.

Задача по выбору индекса довольна сложная, если вообще решаемая. Возможно использовать несколько советов по выбору индекса:
- команда *ANALYZE* для анализа статистических данных в таблице
- использовать реальные данные, а не тестовые
- если индекс используется только по принуждению, может реально не стоит его использовать
- и т.д.

---
### Zero-Links
- 

---
### Links
- [[Индексы (pgsql)]]