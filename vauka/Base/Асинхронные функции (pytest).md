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
- 

---
### Links
- [[Декоратор (py)]]
- [[Unit testing (py)]]
- [[asyncio]]

---
### Outer links
- https://pypi.org/project/pytest-asyncio/