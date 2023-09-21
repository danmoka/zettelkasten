16032023 1351
Tags: #z #dev

---
# Запросы в Django

## exclude

Позволяет отфильтровать данные с условием НЕ. Например, отобрать все автомобили красного цвета, исключив машины 1998 года выпуска:

```python
Car.objects.filter(color='red').exclude(year=1998)
```

Комбинация `exclude().exclude()` равносильна условию ИЛИ. Исключение по нескольким полям `exclude(color='yellow', year=2001`) равносильно условию И.

---
### Zero-Links
- 

---
### Links
- [[Django]]

---
### Outer links
- https://docs.djangoproject.com/en/4.1/ref/models/querysets/