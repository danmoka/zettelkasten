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

---
### Zero-Links
- [[00 aiohttp]]
- [[00 asyncio]]

---
### Links
- [[DI (aiohttp)]]
  
### Outer links
- https://docs.aiohttp.org/en/stable/index.html
- https://docs.aiohttp.org/en/latest/client_advanced.html#persistent-session постоянные сессии
- https://docs.aiohttp.org/en/latest/client_advanced.html продвинутое использование клиента
- https://docs.aiohttp.org/en/stable/web_advanced.html#cleanup-context cleanup_context приложения