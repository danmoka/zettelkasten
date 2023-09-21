17032023 1219
Tags: #z #dev

---
# Асинхронный HTTP клиент

## pip

```shell
pip install aiohttp
```

## Пример

```python
async def main():
	async with aiohttp.ClientSession() as session:
		async with session.get('http://python.org') as response:
			print(response.status)
			print(await response.text())

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

## Использование одной сессии

Работа с сессией делится на два этапа:
- установка сессии
- удаление сессии

```python
async def create_session():
	# установка
	yield
	# удаление

# часть до yield будет вызвана при работе приложение
# часть после - по завершению приложения 
app.cleanup_ctx.append(create_session)
```

Установка сессии:

```python
# чтение конфигурации из настроек (используется DI)
ch_url = current_app.container.config.clickhouse_server()['url']
# установка сессии в текущее приложение
app['CLICKHOUSE'] = ch_session = ClientSession(ch_url, connector=TCPConnector())
```

Удаление сессии:

```python
await ch_session.close()
```

## Использование клиента с политикой повторных вызовов и постоянной сессией

```python
class PersistentSessionHttpClient(HttpClientContract):   
    def __init__(self, retry_attempts: int = 3):  
        self.__exceptions_to_retry = {  
            HTTPClientError,  
            ClientConnectorError  
        }  
        self.__client = RetryClient(retry_options=ExponentialRetry(  
            attempts=retry_attempts,  
            statuses={  
                http.HTTPStatus.TOO_MANY_REQUESTS,  
                http.HTTPStatus.INTERNAL_SERVER_ERROR,  
                http.HTTPStatus.SERVICE_UNAVAILABLE,  
                http.HTTPStatus.GATEWAY_TIMEOUT,  
                http.HTTPStatus.NOT_IMPLEMENTED  
            },  
            exceptions=self.__exceptions_to_retry,  
            start_timeout=1  
        ))  
  
    def __del__(self):  
		# Close connection when this object is destroyed  
        run_sync(self.__client.close)  
  
    async def get(self, url, headers) -> Tuple[int, Optional[bytes]]:   
		async with self.__client.get(url=url, headers=headers) as response:  
			response_data = await response.read()  
			return response.status, response_data  
```

```python
def run_sync(func: Callable[..., Coroutine[Any, Any, None]]) -> None:  
    try:  
        try:  
            loop = asyncio.get_event_loop()  
        except RuntimeError:  
            loop = asyncio.new_event_loop()  
            asyncio.set_event_loop(loop)  
  
        if loop.is_closed():  
            loop = asyncio.new_event_loop()  
            asyncio.set_event_loop(loop)  
  
        if loop.is_running():  
            loop.create_task(func())  
        else:  
            loop.run_until_complete(func())  
    except Exception as exc:  
        logging.getLogger(__name__).warning(exc)
```

---
### Zero-Links
- 

---
### Links
- [[DI (aiohttp)]]
- [[aiohttp]]
  
### Outer links
- https://docs.aiohttp.org/en/stable/index.html
- https://docs.aiohttp.org/en/latest/client_advanced.html#persistent-session постоянные сессии
- https://docs.aiohttp.org/en/latest/client_advanced.html продвинутое использование клиента
- https://docs.aiohttp.org/en/stable/web_advanced.html#cleanup-context cleanup_context приложения
- https://pypi.org/project/aiohttp-retry/ клиент с реализацией политики повторных запросов
- https://stackoverflow.com/questions/54770360/how-can-i-wait-for-an-objects-del-to-finish-before-the-async-loop-closes разбор того, как закрыть сессию в aiohttp