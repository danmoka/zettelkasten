03032023 1217
Tags: #z #dev

---
# Примеры запросов

## Вставка данных

```sql
INSERT INTO TABLE db.tb  
(  
    `timestamp`,
    `brick_id`, 
    `cam_id`,
    `file`,
    `streamer_id`
)  
SELECT *  
FROM (  
    WITH  
        '111111110' AS `brick_id`,  
        2 AS `cam_id`,  
        '11110' AS `file`,  
        2 AS `streamer_id`,  
        toDateTime('2022-09-19 10:00:40') AS `start`,  
        toDateTime('2022-09-19 12:13:00') AS `end`  
    SELECT arrayJoin(arrayMap(x -> toDateTime(x), range(toUInt32(`start`), toUInt32(`end`), 20))) AS `timestamp`, `brick_id`, `cam_id`, `file`, `streamer_id`  
);
```

```sql
INSERT INTO TABLE cctv_click_db.cctv_click_tb  
(  
    `cam_id`,  
    `timestamp`,  
    `brick_id`,  
    `file`,  
    `streamer_id`  
)  
SELECT arrayJoin(arrayMap(x -> x, range(184745, 284744))) AS `cam_id`, `timestamp`, `brick_id`, `file`, `streamer_id`  
FROM (  
	SELECT *  
	FROM (  
	    WITH  
	        '111111110' AS `brick_id`,  
	        '11110' AS `file`,  
	        2 AS `streamer_id`,  
	        toDateTime('2023-03-01 20:56:00') AS `start`,  
	        toDateTime('2023-03-01 20:59:00') AS `end`  
	    SELECT arrayJoin(arrayMap(x -> toDateTime(x), range(toUInt32(`start`), toUInt32(`end`), 20))) AS `timestamp`, `brick_id`, `file`, `streamer_id`  
	)  
);
```

## Выборка

Поиск живых кам.

```sql
SELECT MAX(`timestamp`) as timestamp, `cam_id`  
FROM db.tb  
GROUP BY `cam_id`  
HAVING timestamp > date_sub(second, 60, toDateTime('2023-03-01 22:20:50'))  
ORDER BY timestamp DESC;
```

```sql
SELECT *   
FROM db.tb   
ORDER BY `timestamp` DESC LIMIT 3;
```

## Удаление данных

```sql
ALTER TABLE db.tb DELETE WHERE  brick_id <> '1';
```

---
### Zero-Links
- [[00 ClickHouse]]

---
### Links
- 