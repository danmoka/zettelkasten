01092022 1225
Tags: #z #dev

---
# Локальные переменные

В теле функции переменной можно присвоить значение, такая переменная считается локальной переменной функции.

Аргументы передаются по присваиванию, значит параметры выступают локальными переменными.

Цикл `for` присваивает цели очередной элемент последовательности, цель является локальной переменной.

## def

- Если имени присвоено значение внутри def, то имя видно только внутри функции.
- Имена, объявленные внутри функций, не конфликтуют с именами, объявленными вне функций.
- Имена, объявленные внутри def, доступны вложенным функциям внутри данного def.
- Имена, объявленные за пределами всех def, являются *глобальными в файле*.
- Каждый вызов функции создает новую локальную область видимости.

## global, nonlocal

- Если имя объявлено как `global` внутри функции, то изменение данной переменной изменит глобальную переменную в данном модуле.
- Если имя объявлено как `nonlocal` в функции, то изменение данной переменной изменит переменную объемлющей функции.

```python
def fun1():
	out = 25
	def fun2():
		nonlocal out
		out = 35
```

---
### Zero-Links
- 

---
### Links
- [[for (py)]]
- [[Передача аргументов (py)]]
- [[Функция (py)]]
- [[Область видимости (py)]]
- [[Изучаем Python, Том 1, издание 5, Марк Лутц]] (с. 502, с. 504)