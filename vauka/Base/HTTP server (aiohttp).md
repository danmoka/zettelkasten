17032023 1239
Tags: #z #dev

---
# Асинхронный сервер HTTP 

## pip

```shell
pip install aiohttp
```

## Пример

```python
async def handle(request):
	return web.Response(text='Запрос получен')

app = web.Application()
app.router.add_route('GET', '/', handle)

if __name__ == '__main__':
	web.run_app(app)
```

## Чтение конфигурации

```python
# используется DI
def read_config(container):
	container.config.from_yaml('../config.yml')
```

## Настройка логгера

```yml
log:  
  level: "DEBUG"  
  format: "[%(asctime)s] [%(levelname)s] [%(name)s]: %(message)s"
```

```python
def config_logging(container):
	logging.basicConfig(
		stream=sys.stdout,
		level=container.config.log.level(),
		format=container.config.log.format()
	)
```

## Запуск асинхронных задач вместе с сервером

```python
async def run_async_func(app):
	some_async_func = app.container.some_async_func()
	some_async_task = asyncio.create_task(some_async_func())

	yield

	# таска, получает исключение отмены  
	some_async_task.cancel()  
	  
	with suppress(asyncio.CancelledError):  
	    # ожидаем пока таска остановит выполнение внутри себя
	    # подавляем исключение отмены, выброшенное после остановки внутри таски    
	    await some_async_task
```

```python
app.cleanup_ctx.append(run_async_func)
web.run_app(app=app)
```

---
### Zero-Links
- 

---
### Links
- [[DI (aiohttp)]]
- [[aiohttp]]

---
### Outer links
- https://docs.aiohttp.org/en/stable/web_advanced.html