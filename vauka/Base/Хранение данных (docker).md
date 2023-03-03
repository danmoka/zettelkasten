03032023 1358
Tags: #z #dev

---
# Хранение данных

## Временное хранение

Для временного хранения можно сохранять файлы прямо в слой для записи контейнера. Файлы будут храниться до тех пор, пока существует контейнер.

Можно воспользоваться tmpfs. Файлы будут храниться в оперативной памяти до тех пор, пока запущен контейнер.

## Постоянное хранение

Для постоянного хранения можно использовать тома Docker.
Основные свойства:
- самостоятельны и отделены от контейнеров;
- могут использоваться несколькими контейнерами;
- можно размещать на удаленных ресурсах;
- эффективное чтение и запись.

### Создание тома

Если тома не существует, то он будет создан.

```dockerfile
VOLUME /my_volume
```

Если том существует, то он будет предоставлен для использования в контейнер. Том можно использовать между несколькими контейнерами.

Из командной строки: `docker volume create --name my_volume`

### Пример использования тома

```cmd
docker run -d --name nginx_vol1 -v docker_volume:/usr/share/nginx/html nginx
docker run -d --name nginx_vol2 --mount type=volume,source=docker_volume,destination=/usr/share/nginx/html nginx
```

Два контейнера подключены к том `docker_volume`. Данный том будет доступен по пути /usr/share/nginx/html.

Например, 
```cmd
# создаем файл в одном контейнере 
docker exec nginx_vol1 touch /usr/share/nginx/html/file1
# проверяем файл через другой контейнер 
docker exec nginx_vol2 ls /usr/share/nginx/html
```

### Подключение папок

```cmd
docker run -d --name nginx_vol1 -v /home/alex/docker_data:/usr/share/nginx/html:ro nginx 
# или 
docker run -d --name nginx_vol2 --mount type=bind,source=/home/alex/docker_data,destination=/usr/share/nginx/html,ro nginx
```

Локальная папка /home/alex/docker_data хоста монтируется в контейнер.

>[!note] VOLUME в Dockerfile и в команде docker run
>Стоит различать эти два способа.
>В первом случае (из-за концепции переносимости образов) volume не должен зависеть от хоста. Поэтому указать source и distination не получится. Мы просто создаем (или получаем доступ) к тому и пользуемся им как директорией.
>Во второму случае, мы можем монтировать папки хоста при запуске контейнера (а не во время создания образа).
>Для облегчения монтирования можно воспользоваться docker-compose, где указать source:distination нужных папок хоста.

---
### Zero-Links
- [[00 Docker]]
- second

---
### Links
- 

---
### Outer links
- https://fixmypc.ru/post/sozdaem-volume-v-docker-ispolzuia-bind-i-mount/
- https://habr.com/ru/company/ruvds/blog/441574/