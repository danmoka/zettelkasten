05092022 1451
Tags: #z #dev

---
# Дескрипторы

Дескрипторы - объекты, которые позволяют перехватить (обеспечивает контроль) события получения, доступа, удаления аттрибутов других объектов.

Есть экземпляр дескриптора, который прикреплен к экземпляру клиентского класса.

## Пример

```python
class MyDesc:
    def __get__ (self, instance, owner):
        return instance._my_attr
    def __set__ (self, instance, value):
        raise AttributeError('Can not access')
    def __delete__(self, instance):
        raise AttributeError('Can not access')

class SuperValue:
    def __init__ (self, value):
        self._my_attr = value
    my_attr = MyDesc()
        
sv = SuperValue(123)
print(sv.my_attr) # 123
sv.my_attr = 167 # error...
print(sv.my_attr)
```

---
### Zero-Links
- first
- second

---
### Links
- first
- second