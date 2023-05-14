06042023 1301
Tags: #z #dev 

---
# Тестирование асинхронных функций

## pip

```shell
pip install pytest-asyncio
```

## Декоратор

```python
@pytest.mark.asyncio
async def test_smth():
	res = await some_func()
	assert res
```

---
### Zero-Links
- [[00 Python]]

---
### Links
- [[Декоратор (py)]]

---
### Outer links
- https://pypi.org/project/pytest-asyncio/