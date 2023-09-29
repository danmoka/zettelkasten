04042023 1710
Tags: #z #dev

---
# Декоратор метода класса

## Декоратор в самом классе (не надо так)

```python
class User:
	def update_history(func):
		# ...
```

`update_history` становится методом экземпляра класса, на место `func` передается `self`

## Статический метод (не надо так)

```python
class User:
	@staticmethod
	def update_history(func):
		# ...
```

Применение такого декоратора приведет к возникновению ошибки `TypeError: 'staticmethod' object is not callable`

## Объявление снаружи

```python
def update_history(func):
		# ...

class User:
	def __init__(self, name):
		self._name = name
	
	@update_history
	def change_name(self, name):
		self._name = anme
```

## Объявление во внутреннем классе

```python
class User:
	class Decorators:
		@classmethod
		def update_history(cls, func):
		# ...
	
	def __init__(self, name):
		self._name = name
	
	@Decorators.update_history
	def change_name(self, name):
		self._name = anme
```

---
### Zero-Links
- 

---
### Links
- [[Декоратор (py)]]

---
### Outer links
- https://medium.com/@vadimpushtaev/decorator-inside-python-class-1e74d23107f6