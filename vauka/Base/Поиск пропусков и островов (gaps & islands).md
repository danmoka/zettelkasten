29092023 1452
Tags: #z #dev 

---
# Поиск пропусков и островов

Проблема пробелов и островов заключается в поиске дыр в последовательностях (пробелы) или в поиске диапазонов последовательных значений (острова).

## Поиск пропусков
- отсортировать последовательность
- построить набор данных, состоящий из пар (текущее значение, следующее)
- если разница между текущим и следующим значением больше порогового значения, то найден пропуск

## Поиск островов
- отсортировать последовательность
- построить набор данных (значение, номер в последовательности * пороговое значение)
- номер в последовательности * пороговое значение заменяем на: текущее значение - номер в последовательности * пороговое значение
- для каждого последовательного значения в диапазоне в результате будет возвращена одна и та же дата. Это будет своего рода группировка в острова

---
### Zero-Links
- [[00 PostgreSQL]]

---
### Links
- 

---
### Outer links
- https://www.mssqltips.com/sqlservertutorial/9130/sql-server-window-functions-gaps-and-islands-problem/
- https://www.red-gate.com/simple-talk/databases/sql-server/t-sql-programming-sql-server/gaps-islands-sql-server-data/
- https://www.tinybird.co/blog-posts/tips-9-filling-gaps-in-time-series-on-clickhouse
- https://stackoverflow.com/questions/50238568/how-to-group-by-time-bucket-in-clickhouse-and-fill-missing-data-with-nulls-0s
- https://stackoverflow.com/a/64467534 для клика