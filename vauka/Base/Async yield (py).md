17102023 1215
Tags: #z #dev 

---
# Асинхронный генератор

Асинхронный генератор - это корутина, которая использует выражение *yield*. 

Асинхронный генератор - это функция, которая возвращает асинхронный итератор генератора. С виду - это обычная асинхронная функция, которая возвращает серию ожидаемых объектов, по которой можно итерироваться с помощью асинхронного цикла.

>[!note] Использование
>Асинхронный генератор можно использовать только в асинхронном коде.
>Для перебора значений используется *async for*.
>Для получения следующего значения используется *anext*.

## Пример

```python
# define an asynchronous generator that awaits
async def async_generator():
	for i in range(10)
		await asyncio.sleep(1)
		yield i

async for result in async_generator():
	print(result)
```

---
### Zero-Links
- 

---
### Links
- [[asyncio]]
- [[yield (py)]]

---
### Outer links
- https://superfastpython.com/asynchronous-generators-in-python/