04092022 0912
Tags: #z #dev #quest 

---
# Магические методы

Магические методы - это про объектно-ориентированный Python. Они позволяют наделить класс "магией".

Используя перегрузку магических методов, мы можем перехватывать управление нормальных операций Python и перенаправлять на нашу логику.

Метод | Зачем нужен
------------ | ------------
`__new__` | создает объект экземпляра
`__init__` | инициализация экземпляра 
`__del__` | вызывается при сборке мусора или завершении работы интерпретатора
`__add__` | используется в выражении `+`
`__sub__` | используется в выражении `-`
`__str__` | используется в выводе `print`
`__call__` | вызов объекта как функции
`__setattr__` | установка аттрибута
`__getattr__` | извлечение динамически вычисляемого аттрибута (если его не существует)
`__delattr__` | удаление аттрибута
`__getitem__` | извлечение по индексу/срезу
`__setitem__` | установка по индексу/срезу
`__len__` | проверка длины
`__lt__, __gt__, __le__, __ge__, __eq__, __ne__` | x < y, x > y, x <= y, x >= y, x == y, x != y
`__iter__, __next__` | используются в контексте итерации
`__contains__` | используется для проверки членства `in`
`__get__, __set__, __delete__` | аттрибуты дескриптора

## `__getitem__, __setitem__`

```python
class Indexer:
    def __init__(self, elements):
        self.elements = elements
        
    def __getitem__(self, index):
        print(f'a value is: {self.elements[index]}')
        return self.elements[index]
    
    def __setitem__(self, index, value):
        self.elements[index] = value
        print(f'a new value is: {self.elements[index]}')
        
    def __str__(self):
        return str(self.elements)
        
i = Indexer([1, 2, 3])
i[2]
i[1] = 10
print(i)
# a value is: 3
# a new value is: 10
# [1, 10, 3]
```

## `__iter__, __next__`

```python
class B():
    def __init__(self, collection):
        self.collection = collection
        self.ind = 0
        
    def __next__(self):
        if self.ind < len(self.collection):
            el = self.collection[self.ind]
            self.ind += 1
            return el
        else:
            self.ind = 0
            raise StopIteration()
class A:
    def __init__(self, collection):
        self.collection = collection
    
    def __iter__(self):
        return B(self.collection)
        
        
a = A([1, 2 ,3])

for el in a:
    print(el)
# 1
# 2
# 3
```

## `__getattr__, __setattr__`

```python
class A:
    def __init__(self, collection):
        self.collection = collection
    
    def __setattr__(self, name, value):
        self.__dict__[name] = value
        
    def __getattr__(self, name):
        return f'Вычисляемое значение {name}'
        
        
a = A([1, 2 ,3])
a.collection = [10, 15, 11]
print(a.name)
print(a.collection)

# Вычисляемое значение name
# [10, 15, 11]
```

## `__call__`

```python
def gen(m):
    return lambda x: x * m
    
g2 = gen(2)
print(g2(5)) # 10

class Gen():
    def __init__(self, m):
        self.m = m
        
    def __call__(self, x):
        return self.m * x

g3 = Gen(3)
print(g3(5)) # 15
```

---
### Zero-Links
- 

---
### Links
- [[Классы (py)]]
- [[Изучаем Python, Том 2, издание 5, Марк Лутц]] (с. 124)