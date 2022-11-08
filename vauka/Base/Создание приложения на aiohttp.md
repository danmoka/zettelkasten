08112022 1502
Tags: #z #dev

---
# Создание приложения на aiohttp

Используя uvloop и gunicorn получаем достаточно быстрое асинхронное приложение, использующее несколько воркеров для работы.

## Создание структуры

- создать папку для проекта (в данной папке будут лежать файлы конфигурации, .gitignore, docker-compose.yml, папка приложения и т.д.)
- создать папку приложения (где будут основные файлы по типу main.py и папки для работы с основными сущностями)
- в папке с сущностями создать папки (base, mappers, validators, services, repositories, controllers и т.д.)
- определить папки для контрактов для реализации DI

- project
    - app
        - event
            - base
                - utils.py
            - mappers
                - event_mapper.py
            - validators
            - services
                - contracts
                    - base_repository.py
            - repositories
            - views
            - main.py
            - middleware.py
            - routes.py
        - user
    - docker-compose.yml
    - .gitignore
    - .env
    - requirements.txt
    - README.md


## .gitignore

Заполняется стандартными данными согласно готовым файлам из сети Интернет. Дополняется данными для сокрытия файлов конфигурации (.env, **config.yaml и т.д.)

## Запуск с uvloop без gunicorn

Dokerfile

```Dockerfile
FROM python:3.7

WORKDIR /source

COPY ["requirements.txt", "requirements.txt"]
COPY ["config/prod/config.yaml", "./config/config.yaml"] # подставляем продовские настройки

RUN pip3 install -r requirements.txt
RUN pip3 install uvloop

COPY ["app", "./app"]

CMD [ "python", "app/main.py"]
```

## Запуск с uvloop с gunicorn

Используя .env можно указать docker-compose какой Dockerfile брать.

Dockerfile

```Dockerfile
FROM python:3.7

WORKDIR /source

COPY ["requirements.txt", "requirements.txt"]
COPY ["config/prod/", "./config"] # в папке прода должен лежать файл gunicorn.conf с настройками gunicorn

RUN pip3 install -r requirements.txt
RUN pip3 install uvloop
RUN pip3 install gunicorn

COPY ["app", "./app"]

CMD [ "gunicorn", "-c", "./config/gunicorn.conf", "main:app_factory" ]
```

## docker-compose

В данном примере приложение app связано с прокси сервером ClickHouse-bulk для накопления данных для вставки. Прокси связан с самой базой ClickHouse. Данные пароля и логина скрыты в .env файле.

```yml
version: "3.9"
services:
  app:
    image: app
    build:
      context: ./
      dockerfile: "${DOCKER_FILE_PATH}"
    ports:
      - "8080:8080"
    depends_on:
      - clickhouse-bulk
  clickhouse-bulk:
    image: nikepan/clickhouse-bulk
    ports:
      - "8124:8124"
    environment:
      - CLICKHOUSE_SERVERS=http://clickhouse-server:8123
      - CLICKHOUSE_FLUSH_INTERVAL=1000
      - CLICKHOUSE_BULK_DEBUG=no
      - CLICKHOUSE_INSECURE_TLS_SKIP_VERIFY=true
    depends_on:
      - clickhouse-server
  clickhouse-server:
    image: clickhouse/clickhouse-server
    ports:
      - "8123:8123"
      - "9000:9000"
    env_file:
      - '.env'
```

## Советы

Хорошим тоном будет создать один файл с переменными (yaml или .env). Удобнее контролировать, удобнее заполнять. Проще подставлять данные в ci/cd.

---
### Zero-Links
- [[00 Python]]

---
### Links
- 