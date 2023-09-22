22092023 0836
Tags: #z #dev 

---
# Фикстуры

Фикстуры - это функции, которые могут выполняться до (а иногда и после) теста, приводя систему к нужному состоянию, и предоставляя тестовые данные.

## Пример

```python
import pytest 

@pytest.fixture
def some_data():
	return 42

def test_some_data(some_data):
	assert some_data == 42
```

## Пример в асинхронном коде

```python
import pytest
import pytest_asyncio
import asyncio

@pytest_asyncio.fixture
async def some_data():
	await asyncio.sleep(0.1)
	return 42

@pytest.mark.asyncio
async def test_some_data(some_data):
	assert some_data == 42
```

## Передача параметров

```python
import pytest 

@pytest.fixture
def some_data(value1, value2):
	return value * 2

@pytest.mark.parametrize(['value1', 'value2'], [(1, 2)])
def test_some_data(some_data, value1, value2):
	assert some_data == 42
```

## Выполнение кода ДО и ПОСЛЕ теста

```python
import asyncio
import pytest
import pytest_asyncio

@pytest_asyncio.fixture 
async def good_fixture():
    await asyncio.sleep(0) # код ДО
    yield 'good_fixture_value'
    await asyncio.sleep(0) # код ПОСЛЕ

@pytest.mark.asyncio
async def test_good_fixture(good_fixture):
    assert good_fixture == 'good_fixture_value'
```

## conftest.py

Данный модуль можно определить на уровне пакета с тестами. Фикстуры из данного модуля можно использовать в разных тестах. Для определения области действия фикстура, можно использовать *scope* (function, class, module, package or session).

---
### Zero-Links
- first
- second

---
### Links
- [[Асинхронные функции (pytest)]]
- [[Unit testing (py)]]
- [[yield (py)]]

### Outer links
- https://stackoverflow.com/questions/49936724/async-fixtures-with-pytest
- https://stackoverflow.com/questions/18011902/how-to-pass-a-parameter-to-a-fixture-function-in-pytest
- https://docs.pytest.org/en/6.2.x/fixture.html#conftest-py-sharing-fixtures-across-multiple-files
- https://stackoverflow.com/questions/74351637/pytest-with-async-tests-test-setup-before-and-after
- https://habr.com/ru/articles/448786/