22092023 1018
Tags: #z #dev 

---
# asyncio.as_completed

Данная функция позволяет одновременно запустить множество задач или корутин и получить результаты выполнения в порядке их завершения. Возвращает итератор, значениями которого являются корутины. Ожидая корутины, можно получить результат выполнения (или исключение).

## Пример с задачами

```python
# SuperFastPython.com

from random import random
import asyncio

# coroutine to execute in a new task
async def task_coro(arg):
    value = random()
    await asyncio.sleep(value)

    return arg * value

async def main():
    coros = [asyncio.create_task(task_coro(i)) for i in range(10)]

    # get results as tasks are completed
    for future in asyncio.as_completed(coros):

        # get the result from the next task to complete
        result = await future
        print(f'>got {result}')

# start the asyncio program
asyncio.run(main())
```

- main() корутина выполняется и создает набор задач
- каждая задача запланирована для независимого запуска после создания
- main() корутина передает набор задач в as_completed
- as_completed возвращает генератор, каждая итерация по которому возвращает корутину
- ожидание корутины блокирует main() корутину
- main() корутина получает вычисленный результат

>[!note] Исключения
>Код ожидания результата выполнения корутины лучше обернуть в try..except, т.к. необработанное исключение завершает программу asyncio и завершает основной поток

---
### Zero-Links
- 

---
### Links
- [[asyncio]]
- [[create_task]]

---
# Outer links
- https://superfastpython.com/asyncio-as_completed/
- https://stackoverflow.com/questions/44049719/how-does-asyncio-as-completed-work