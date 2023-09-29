29092023 1515
Tags: #z #dev

---
# Контекстный менеджер

## Как метода класса/экземпляра

```python
import contextlib

class Foo:
    @classmethod
    @contextlib.contextmanager
    def state1(cls):
        try:
            print("A")
            yield
            print("C")
        finally:
            pass
    
    @contextlib.contextmanager
    def state2(self):
        try:
            print("A")
            yield
            print("C")
        finally:
            pass

with Foo.state1():
    print("B")

foo = Foo()

with foo.state2():
	print("B")
```

---
### Zero-Links
- [[00 Python]]

---
### Links
- [[Декоратор метода класса (py)]]

---
### Outer links
- https://stackoverflow.com/questions/73951746/how-to-use-contextlib-contextmanager-with-a-classmethod
- https://stackoverflow.com/questions/35350897/python-standard-function-and-context-manager