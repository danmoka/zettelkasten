29092023 1540
Tags: #z #dev

---
# Запуск и завершение асинхронного приложения

```python
import asyncio  
import platform  
import signal  
    
from my_app.startup import startup
from my_app.dispatcher import Dispatcher
  
  
def main() -> None:  
    # установка цикла событий  
    loop = asyncio.new_event_loop()  
    asyncio.set_event_loop(loop)  
    # настройка приложения (всё, что угодно)
    startup()  
  
    # диспетчер задач  
    dispatcher = Dispatcher()  
  
    # если платформа поддерживает сигналы  
    if platform.system() == 'Linux' or platform.system() == 'Darwin':  
        # добавление обработчика закрытия диспетчера задач для цикла событий  
        loop.add_signal_handler(
	        signal.SIGTERM, lambda: loop.create_task(dispatcher.stop())
        )  
        loop.add_signal_handler(
	        signal.SIGINT, lambda: loop.create_task(dispatcher.stop())
        )  
  
    try:  
        # запуск выполнения задач диспетчера  
        loop.run_until_complete(dispatcher.start())  
    except (SystemExit, KeyboardInterrupt):  
        pass  
    finally:  
        loop.run_until_complete(dispatcher.stop())  
        loop.run_until_complete(loop.shutdown_asyncgens())  
        loop.close()  
        asyncio.set_event_loop(None)  
  
  
if __name__ == '__main__':  
    main()
```

*startup* - настройка приложения, можно передать *loop*, если требуется асинхронная настройка
*dispatcher* - диспетчер задач, который умеет корректно запускать и останавливать задачи

>[!note] Сигналы
>Если система поддерживает сигналы, то добавляем в цикл событий задачи на сигналы прерывания работы

>[!note] Исключения
>Если возникло исключение-прерывание, то выполняем задачу по остановке диспетчера, закрываем и очищаем цикл событий

---
### Zero-Links
- 

---
### Links
- [[asyncio]]

