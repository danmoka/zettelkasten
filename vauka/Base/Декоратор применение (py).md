05042023 1337
Tags: #z #dev
---
# Применение декораторов

## @logger

Логгирует вызов функции

```python
def logger(func):
	def wrapper(*args, **kwargs):
		logging.getLogger().info('start')
		return func(*args, **kwargs)
		logging.getLogger().info('end')
	return wrapper
```

## @wraps

Для корректного отображения документации по декорируемой функции

```python
def logger(func):
	@wraps(func)
	def wrapper(*args, **kwargs):
		logging.getLogger().info('start')
		return func(*args, **kwargs)
		logging.getLogger().info('end')
	return wrapper
```

## @lru_cache

Кеширует возвращаемые значения

```python
@lru_cache(max_size=None)
def heavy_process(n):
	time.sleep(n + random.random())
```


## @time_it

Считает время выполнения функции

```python
def time_it(func):
	@wraps(func)
	def wrapper(*args, **kwargs):
		start = time.perf_counter()
		result = func(*args, **kwargs)
		end = time.perf_counter()
		print(f'{func.__name__} took {end - start:.6f} seconds to complete')
		
		return result
	return wrapper 
```

## @retry

Повторный вызов функции при возникновении определенных ошибок

```python
def retry(num_tries, exc_to_check, sleep_time=0):
	def decorate(func):
		@wraps(func)
		def wrapper(*args, **kwargs):
			for i in range(num_tries):
				try:
					return func(*args, **kwargs)
				except exc_to_check as exc:
					if i < num_retries:
						time.sleep(sleep_time)
			raise Exception
		return wrapper
	return decorate
```

## @limits

Ограничивает количество вызовов за определенный период. Превышение лимита вызовов генерирует `ratelimit.RateLimitException`

```python
from ratelimit import limits
import requests

@limits(calls=15, period=300)
def call_api(url):
	return requests.get(url)
```

## @dataclass

Декорирует классы. Автоматически генерирует методы `__init__`, `__repr__`, `__eq__`, `__lt__` , `__str__`. Делает объекты неизменяемыми, конвертируемыми в JSON.

## @property

Реализация getter'ов и setter'ов

```python
class User:
	def __init__(self, name):
		self._name = name

	@property
	def name(self):
		return self._name

	@name.setter
	def name(self, name):
		self._name = name
```

---
### Zero-Links
- 

---
### Links
- [[Декоратор (py)]]

---
### Outer links
- https://towardsdatascience.com/12-python-decorators-to-take-your-code-to-the-next-level-a910a1ab3e99