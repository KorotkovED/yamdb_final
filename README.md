# yamdb_final
[![Python](https://img.shields.io/badge/-Python-464641?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Pytest](https://img.shields.io/badge/-Pytest-464646?style=flat-square&logo=pytest)](https://docs.pytest.org/en/6.2.x/)
![workflow](https://github.com/github/docs/actions/workflows/main.yml/badge.svg)


Яндекс Практикум. Проект 16-го спринта: CI и CD проекта api_yamdb.

## Описание

Проект `YaMDb` собирает отзывы пользователей на произведения из категорий: «Книги», «Фильмы», «Музыка».

## Функционал

- Произведения делятся на категории. Список категорий может быть расширен администратором;
- Произведения, фильмы и музыка не хранятся в приложении;
- В каждой категории есть произведения: книги, фильмы или музыка;
- Произведению может быть присвоен жанр из списка предустановленных. Новые жанры может создавать только администратор;
- Пользователи могут оставлять отзывы и ставить оценку произведениям. Из пользовательских оценок формируется рейтинг. На одно произведение можно оставить только один отзыв.

## Установка

1. Клонировать репозиторий:

    ```python
    git clone git@github.com:KorotkovED/yamdb_final.git
    ```

2. Создать `.env` файл на уровне с файлом `docker-compose.yaml` в директории infra с указаниме данных:

    - SECRET_KEY - секретный ключ Django;
    - DB_ENGINE - движок базы данных (БД) postgresql: `django.db.backends.postgresql`;
    - DB_NAME - имя БД: `yatube`;
    - POSTGRES_USER - пользователь БД: `yatube_user`;
    - POSTGRES_PASSWORD - пароль рользователя БД: `xxxyyyzzz`;
    - DB_HOST - адрес удалённого сервера БД, по умолчанию: `127.0.0.1`;
    - DB_PORT - порт сервера базы данных: `5432`;

3. Создать и активировать виртуальное пространство, установить зависимости и запустить тесты:

    Для Windows:

    ```python
    cd yamdb_final
    python -m venv venv
    source venv/Scripts/activate
    cd api_yamdb
    pip install -r requirements.txt
    cd ..
    pytest
    ```

    Для Mac/Linux:

    ```python
    cd yamdb_final
    python3 -m venv venv
    source venv/bin/activate
    cd api_yamdb
    pip install -r requirements.txt
    cd ..
    pytest
    ```

4. Запустить контейнер Docker:

    - Проверить статус Docker:

    ```python
    docker --version
    ```

    - Запустить docker-compose:

    ```python
    cd infra/
    docker-compose up -d
    ```

5. Выполнить миграции, создать суперпользователя и мигрировать статику:

    ```python
    docker-compose exec web python manage.py migrate
    docker-compose exec web python manage.py createsuperuser
    docker-compose exec web python manage.py collectstatic --no-input
    ```

6. Для запуска в виртуальном окружении, после создания и активации виртуального пространства, установки зависимостей, запустить проект локально:

    Для Windows:

    ```python
    python manage.py runserver
    ```

    Для Mac/Linux:

    ```python
    python3 manage.py runserver
    ```

7. Проверить доступность сервиса:

    ```python
    http://localhost/admin
    http://51.250.2.164/admin
    ```
