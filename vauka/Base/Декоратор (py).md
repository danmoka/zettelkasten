08112022 1436
Tags: #z #dev

---
# Декораторы

## Декоратор асинхронной функции

Почти не отличается от обычно декоратора.

```python
def dec(func):
    @functools.wraps(func)
    async def wrapper(*args, **kwargs):
        print('Wrapper start...')
        res = await func(*args, **kwargs)

        return res

    return wrapper
```

## Декоратор метода (с ссылкой на экземпляр)

```python
def dec(func):
    def wrapper(self, *args, **kwargs):
        print('Wrapper start...')
        print(f'Color is {self.color}')
        res = func(self, *args, **kwargs)
        return res
    
    return wrapper
```

---
### Zero-Links
- 

---
### Links
- [[Функция (py)]]