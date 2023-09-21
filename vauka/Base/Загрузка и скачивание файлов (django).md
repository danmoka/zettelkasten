16032023 1403
Tags: #z #dev

---
# Методы API для загрузки и скачивания файлов

## Загрузка (upload) (кто-то загружает файлы через API)

Для того, чтобы получить загружаемые файлы требуется обратиться к атрибуту FILES в запросе:

```python
request.FILES.get('file')
```

Таким образом, можно получить доступ к коллекции файлов, которые лежат в запросе по ключу `file`.

## Скачивание (download) (кто-то скачивает файлы через API)

Для того, чтобы отдать файл в ответе, требуется использовать FileResponse:

```python
FileResponse(open('путь до файла', 'rb'), as_attachment=True)
```

---
### Zero-Links
- 

---
### Links
- [[Django]]
  
---
### Outer links
- https://docs.djangoproject.com/en/4.1/topics/http/file-uploads/
- https://docs.djangoproject.com/en/4.1/ref/request-response/#fileresponse-objects