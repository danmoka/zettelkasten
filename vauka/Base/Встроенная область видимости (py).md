01092022 1653
Tags: #z #dev 

---
# Встроенная область видимости

Встроенная область видимости - это всего лишь модуль, содержащий набор имен и функций.
Для того, чтобы получить доступ к именам, как и обычно, требуется импортировать модуль, а затем обратиться к именам данного модуля.

Но, т.к. последняя стадия поиска имен - это поиск во встроенной области видимости, то модуль можно не импортировать.

## Переопределение встроенных имен

>[!danger] Зачастую это опасная ошибка
>Хотя это незапрещено, но может привести к ошибкам. В локальной области видимости можно переопределить как глобальное имя, так и встроенное.

```python
def fun():
    open = 'spam
    file = open('text.txt', 'r')
    # будет выброшено исключение
```

---
### Zero-Links
- 

---
### Links
- [[Область видимости (py)]]
- [[Изучаем Python, Том 1, издание 5, Марк Лутц]] (с. 512)