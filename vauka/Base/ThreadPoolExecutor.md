22092023 1215
Tags: #z #dev

---
# Менеджер потоков

ThreadPoolExecutor - это менеджер потоков, который позволят создавать потоки и управлять ими.

## Пример

```python
import concurrent.futures
from time import sleep

def func(n):
	sleep(n)

	return n

with concurrent.futures.ThreadPoolExecutor() as exe:  
     tasks = [exe.submit(func, i) for i in range(5)]
        
        for future in concurrent.futures.as_completed(tasks):
            print(future.result())
```

##  Пример использования генераторов в пуле потоков

```python
import concurrent.futures
from time import sleep
from datetime import datetime

# эмуляция медленной функции удвоения числа
def double_it(number):
    sleep(1)
    doubled_number = number * 2
    
    return doubled_number

# генератор удвоенных чисел
def double_it_gen(numbers):
    for number in numbers:
        yield double_it(number)

# список удвоенных чисел        
def double_it_list(numbers):
    res = []
    
    for number in numbers:
        res.append(double_it(number))
        
    return res
    
# запуск обработки пачек чисел в разных потоках
def batch_run(numbers_batches, func):
    with concurrent.futures.ThreadPoolExecutor() as exe:
        tasks = [exe.submit(func, numbers_batch) for numbers_batch in numbers_batches]
        
        for future in concurrent.futures.as_completed(tasks):
            yield future.result()

numbers_batches=[[1, 2, 3], [7, 8, 9], [10, 10, 10]]
            
print('Генерация чисел в разных потоках с помощью генератора')
start = datetime.now()

for doubled_numbers in batch_run(numbers_batches, double_it_gen):
    for doubled_number in doubled_numbers:
        print(doubled_number)

stop = datetime.now()
print((stop - start).total_seconds())

print('Генерация чисел в одном потоке с помощью генератора')
start = datetime.now()

for batch in numbers_batches:
    for doubled_number in double_it_gen(batch):
        print(doubled_number)

stop = datetime.now()
print((stop - start).total_seconds())

print('Генерация чисел в разных потоках с помощью списка')
start = datetime.now()

for doubled_numbers in batch_run(numbers_batches, double_it_list):
    for doubled_number in doubled_numbers:
        print(doubled_number)
        
stop = datetime.now()
print((stop - start).total_seconds())

print('Генерация чисел в одном потоке с помощью списка')
start = datetime.now()

for batch in numbers_batches:
    for doubled_number in double_it_list(batch):
        print(doubled_number)
        
stop = datetime.now()
print((stop - start).total_seconds())
```

>[!note] Возвращение генератора из потока
>Возвращение генератора из потока не дает плюшек по параллельной обработке, т.к. генератор вычисляется сразу, как отрабатывает инструкция yield. Таким образом, получаем параллельно генераторы, а числа вычисляются уже при итерации по генератору.

## Обработка ошибок

Обработать ошибки в потоке можно следующим образом:
- в самой функции, запускаемой в потоке
- при получении результата, вызвав *future.result()*
- вызвать метод *future.exception()*

---
### Zero-Links
- [[00 Python]]

---
### Links
- [[yield (py)]]

---
### Outer links
- https://superfastpython.com/threadpoolexecutor-exception-handling/#Exception_Handling_in_Task_Execution
- https://superfastpython.com/threadpoolexecutor-in-python/
- https://stackoverflow.com/questions/6324318/yield-item-from-a-thread
- https://stackoverflow.com/questions/48724986/how-do-i-use-threads-on-a-generator-while-keeping-the-order