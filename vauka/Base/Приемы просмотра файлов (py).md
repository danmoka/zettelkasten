31082022 1702
Tags: #z #dev

---
# Приемы просмотра файлов
Проблема: загрузка файла целиком в память.
Решение: чтение из файла посимвольно или построчно.

## Примеры плохого чтения

```python
# чтение всего файла сразу
for char in open('text.txt').read():
    print(char)

# чтение всех строк файла сразу
for line in open('text.txt').readlines():
    print(line.rstrip())
```

## Пример хорошего чтения

```python
file = open('text.txt', 'rb')

while True:
    line = file.readline()
    # char = file.read(1)
    
    if not line:
        break

    print(line.rstrip())

# пока лучший вариант, использует файловый итератор, который возвращает строки по одной
for line in open('text.txt'):
    print(line.rstrip())
```

---
### Zero-Links
- [[Циклы (py)]]

---
### Links
- [[for (py)]]
- [[while (py)]]