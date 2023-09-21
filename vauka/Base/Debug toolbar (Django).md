13032023 1256
Tags: #z #dev

---
# Debug toolbar

Как включить:
- добавить установленные приложения:
  ```python
  INSTALLED_APPS = ['django.contrib.staticfiles',  'debug_toolbar']
  ```
- добавить промежуточное ПО:
  ```python
  MIDDLEWARE = ['debug_toolbar.middleware.DebugToolbarMiddleware']
  ```
- внутренний IP:
  ```python
  INTERNAL_IPS = ['127.0.0.1']
  ```
- шаблоны:
  ```python
  TEMPLATES = [{
	'BACKEND': 'django.template.backends.django.DjangoTemplates',  
	'APP_DIRS': True,  
	}]
  ```
- статика:
  ```python
  STATIC_URL = 'static/'
  ```
- cctv_api/urls.py
  ```python
  urlpatterns = [path('__debug__/', include('debug_toolbar.urls'))]
  ```

---
### Zero-Links
- 

---
### Links
- [[Django]]

---
### Outer links
- https://django-debug-toolbar.readthedocs.io/en/latest/