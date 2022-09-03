03092022 1216
Tags: #z #dev

---
# Модули для работы с файлами

## pickle

Модуль pickle позволяет сериализовать и десериализовать объекты.

```python
import pickle
d = { 'a': 1, 'b': 2 }
f = open('file.pkl', 'wb')
pickle.dumps(d, f)
f.close()

f = open('file.pkl', 'rb')
d = pickle.load(f)
```

## json

JSON - более универсальный формат, не зависит от языка программирования.

```python
import json
d = { 'a': 1, 'b': 2}
j = json.dumps(d)
print(j) # '{ "a": 1, "b": 2 }'
d2 = json.loads(j)
d2 == d # True
```

---
### Zero-Links
- 

---
### Links
- [[Операции над файлами (py)]]
- [[Изучаем Python, Том 1, издание 5, Марк Лутц]] (с. 317)