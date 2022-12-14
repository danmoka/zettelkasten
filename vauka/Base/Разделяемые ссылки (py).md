02092022 1225
Tags: #z #dev

---
# Разделяемые ссылки в Python

В Python нет возможности присвоить одну переменную другой.

## Неизменяемые типы
```python
a = 3
b = a
```

В данном коде имени `а` присваивается объект 3 в памяти. При выполнении второй строки имя `a` заменяется на объект из памяти. Таким образом, `b` ссылается на объект 3 в памяти. При этом `a` и `b` никак не связаны, кроме как тем, что ссылаются на одно и тоже место в памяти. Такой объект в памяти называется разделяемым объектом или разделяемой ссылкой

## Изменяемые типы

```python
l1 = [1, 2, 3]
l2 = l1
l1 = 5
# l2 = [1, 2, 3]
```

В данном коде l1 ссылается на объект списка, как и l2. Третья строка присваивает l1 новый объект, при этом l2 продолжает ссылаться на объект списка.

```python
l1 = [1, 2, 3]
l2 = l1
l1[0] = 5
# l2 = [5, 2, 3]
```

Список хранит в себе ссылки на другие объекты. В третье строке заменили объект списка по индексу 0 на другой объект. Сам объект-список остался. Поэтому l1 и l2 продолжают ссылаться на один и тот же объект списка.

>[!note] Количество ссылок на объект
```python
sys.getrefcount(obj)
```
---
### Zero-Links
- 

---
### Links
- [[Типы данных (py)]]
- [[Изучаем Python, Том 1, издание 5, Марк Лутц]] (с. 212)