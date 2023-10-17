17032023 1242
Tags: #z #dev

---
# Инверсия зависимостей в приложениях aiohttp

## DIP

Принцип инверсии зависимостей позволяет настроить правильное направление зависимостей в отношениях компонентов: детали зависят от абстракций, а также детали зависят от БЛ, а не наоборот.

## pip

```txt
dependency-injector
aiohttp
pyyaml
```

```shell
pip install -r requirements.txt
```

## Контейнер

```python
class ApplicationContainer(containers.DeclarativeContainer):
	config = providers.Configuration()
```

Настройку контейнера можно вынести в отдельные функции: настройка логгера, конфига, демонов, мониторов, вью и т.д.
Предпочтительнее все экземпляры подставлять сразу и в одном месте, например, в методе `startup`, который внедряет зависимости, чем использовать инжектирование (так больше порядка).

## Настройка вью и путей

```python
def config_routes(app):  
    daemon_view = app.container.daemon_view()  
    app.router.add_route('GET', '/v1/check/', daemon_view.check)
```

---
### Zero-Links
- 

---
### Links
- [[DIP (архитектура)]]
- [[aiohttp]]

---
### Outer links
- https://habr.com/ru/post/514384/ DI + aiohttp