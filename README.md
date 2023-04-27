# Запуск docker-compose проекта API_YAMDB
### Описание
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

### Технологии

* Python 3.7

* Django 2.2

* DRF 

* JWT + Djoser

* Postgresql

* Docker

* NGINX

# Запуск проекта
## Dev-режим:
- Клонируйте репозиторий и перейдите в него в командной строке.
```
git clone https://github.com/golenkovyura/infra_sp2
```
- Установите виртуальное окружение c версии Python 3.7 :
```
python -m venv venv
```
- Активируйте виртуальное окружение :

```
source venv/Scripts/activate
```

- Перейдите в директорию yatube_api и установите зависимости из файла requirements.txt:
```
cd api_yamdb

pip install -r requirements.txt
```
- Выполните миграции:
```
python manage.py makemigrations

python manage.py migrate
```
- После требуется создать суперпользователя:
```
python manage.py createsuperuser
```
- Чтобы запустить проект используйте команду:
```
python manage.py runserver
```
## Docker-compose:

- Шаблон наполнения .env расположенный по пути infra/.env
```bash
DB_ENGINE=<...> # указываем, что работаем с postgresql
DB_NAME=<...> # имя базы данных
POSTGRES_USER=<...> # логин для подключения к базе данных
POSTGRES_PASSWORD=<...> # пароль для подключения к БД (установите свой)
DB_HOST=<...> # название сервиса (контейнера)
DB_PORT=<...> # порт для подключения к БД 
```

### Запуск

- Переходим в папку с docker-compose:
```bash
cd infa
```
- Запустите контейнер:
```bash
docker-compose up -d --build 
```
- Выполните миграции:
```bash
docker-compose exec web python manage.py makemigrations

docker-compose exec web python manage.py migrate
```
- Создайте суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```
- Соберите статику:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```