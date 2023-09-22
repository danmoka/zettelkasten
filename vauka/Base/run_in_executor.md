22092023 1204
Tags: #z #dev

---
# Запуск множества синхронных задач

Для запуска множества долгих (или нагружающих систему) синхронных задач в асинхронном коде можно использовать метод *run_in_executor*.
Для использования *run_in_executor* требуется текущий *event loop*.

## Пример

```python
import asyncio
import time

def blocking_task():
    time.sleep(2)

async def main():
    awaitalbes = [loop.run_in_executor(None, blocking_task) for _ in range(5)]  
  
	for future in asyncio.as_completed(awaitalbes):  
	    try:  
	        await future  
	    except Exception as exc:  
	        print(str(exc))
	        continue

asyncio.run(main())
```

>[!note] None
>Если в качестве исполнителя передано None, то используется исполнитель по умолчанию - **ThreadPoolExecutor**

---
### Zero-Links
- 

---
### Links
- [[asyncio]]
- [[ThreadPoolExecutor]]
- [[as_completed]]

---
### Outer links
- https://stackoverflow.com/questions/21159103/what-kind-of-problems-if-any-would-there-be-combining-asyncio-with-multiproces
- https://stackoverflow.com/questions/28492103/how-to-combine-python-asyncio-with-threads
- https://superfastpython.com/asyncio-blocking-tasks/
- https://stackoverflow.com/questions/65768399/does-a-loop-run-in-executor-functions-need-asyncio-lock-or-threading-lock