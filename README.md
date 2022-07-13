## Технологический стек
[![Django-app workflow](https://github.com/pupersa23/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/pupersa23/yamdb_final/actions/workflows/yamdb_workflow.yml)
[![Python](https://img.shields.io/badge/-Python-464646?style=flat&logo=Python&logoColor=56C0C0&color=008080)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat&logo=Django&logoColor=56C0C0&color=008080)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat&logo=Django%20REST%20Framework&logoColor=56C0C0&color=008080)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat&logo=PostgreSQL&logoColor=56C0C0&color=008080)](https://www.postgresql.org/)
[![JWT](https://img.shields.io/badge/-JWT-464646?style=flat&color=008080)](https://jwt.io/)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat&logo=NGINX&logoColor=56C0C0&color=008080)](https://nginx.org/ru/)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat&logo=gunicorn&logoColor=56C0C0&color=008080)](https://gunicorn.org/)
[![Docker](https://img.shields.io/badge/-Docker-464646?style=flat&logo=Docker&logoColor=56C0C0&color=008080)](https://www.docker.com/)
[![Docker-compose](https://img.shields.io/badge/-Docker%20compose-464646?style=flat&logo=Docker&logoColor=56C0C0&color=008080)](https://www.docker.com/)
[![Docker Hub](https://img.shields.io/badge/-Docker%20Hub-464646?style=flat&logo=Docker&logoColor=56C0C0&color=008080)](https://www.docker.com/products/docker-hub)
[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat&logo=GitHub%20actions&logoColor=56C0C0&color=008080)](https://github.com/features/actions)
[![Yandex.Cloud](https://img.shields.io/badge/-Yandex.Cloud-464646?style=flat&logo=Yandex.Cloud&logoColor=56C0C0&color=008080)](https://cloud.yandex.ru/)

# Проект YaMDb
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Title). Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список категорий (Category) может быть расширен.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории "Книги" могут быть произведения "Винни Пух и все-все-все" и "Марсианские хроники", а в категории "Музыка" — песня "Давеча" группы "Насекомые" и вторая сюита Баха. Произведению может быть присвоен жанр из списка предустановленных (например, "Сказка", "Рок" или "Артхаус"). Новые жанры может создавать только администратор.
Благодарные или возмущённые читатели оставляют к произведениям текстовые отзывы (Review) и выставляют произведению рейтинг.


# Ресурсы API YaMDb
**AUTH**: аутентификация.

**USERS**: пользователи.

**TITLES**: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).

**CATEGORIES**: категории (типы) произведений ("Фильмы", "Книги", "Музыка").

**GENRES**: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.

**REVIEWS**: отзывы на произведения. Отзыв привязан к определённому произведению.

**COMMENTS**: комментарии к отзывам. Комментарий привязан к определённому отзыву.

# Алгоритм регистрации пользователей
Пользователь отправляет POST-запрос с параметром email на `/api/v1/auth/email/`.
YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email (функция в разработке).
Пользователь отправляет POST-запрос с параметрами email и confirmation_code на `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен).
Эти операции выполняются один раз, при регистрации пользователя. В результате пользователь получает токен и может работать с API, отправляя этот токен с каждым запросом.

# Пользовательские роли
**Аноним** — может просматривать описания произведений, читать отзывы и комментарии.

**Аутентифицированный пользователь (user)** — может читать всё, как и Аноним, дополнительно может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии.

**Модератор (moderator)** — те же права, что и у Аутентифицированного пользователя плюс право удалять и редактировать любые отзывы и комментарии.

**Администратор (admin)** — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.

**Администратор Django** — те же права, что и у роли Администратор.

# Установка

**Шаг 1.** Проверьте установлен ли у вас Docker
Прежде, чем приступать к работе, необходимо знать, что Docker установлен. Для этого достаточно ввести:

    docker -v

Или скачайте Docker Desktop для Mac или Windows. Docker Compose будет установлен автоматически. В Linux убедитесь, что у вас установлена последняя версия Compose. Также вы можете воспользоваться официальной инструкцией.

**Шаг 2.** Клонируйте репозиторий себе на компьютер
Введите команду:

    git clone git@github.com:pupersa23/infra_sp2.git

**Шаг 3.** Создайте в клонированной директории файл .env

Пример:

    DB_ENGINE=django.db.backends.postgresql
    DB_NAME=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=postgres
    DB_HOST=db
    DB_PORT=5432

**Шаг 4.** Запуск docker-compose
Для запуска необходимо выполнить из директории с проектом команду:

    docker-compose up -d

**Шаг 5.** База данных
Создаем и применяем миграции:

    docker-compose exec web python manage.py makemigrations --noinput
    docker-compose exec web python manage.py migrate --noinput

**Шаг 6.** Подгружаем статику
Выполните команду:

    docker-compose exec web python manage.py collectstatic --no-input 

**Шаг 7.** Заполнение базы тестовыми данными
Для заполнения базы тестовыми данными вы можете использовать файл fixtures.json, который находится в infra_sp2. Выполните команду:

    docker-compose exec web python manage.py loaddata fixtures.json

**Другие команды**

Создание суперпользователя:

    docker-compose exec web python manage.py createsuperuser

Остановить работу всех контейнеров можно командой:

    docker-compose down

Для пересборки и запуска контейнеров воспользуйтесь командой:

    docker-compose up -d --build 

Мониторинг запущенных контейнеров:

    docker stats

Останавливаем и удаляем контейнеры, сети, тома и образы:

    docker-compose down -v

**Примеры**

Получаем confirmation_code

Для формирования запросов и ответов использована программа Postman.

Отправляем POST-запрос на адрес http://127.0.0.1/api/v1/auth/email/

Обязательное поле: email
POST   http://127.0.0.1/api/v1/auth/email/
Content-Type: application/json

    {
        "email": "<EMAIL>"
    }

Код подтверждения будет доступен по адресу api_yamdb\sent_emails\file.log

Получаем token
Отправляем POST-запрос для получения JWT-токена на адрес http://127.0.0.1/api/v1/auth/token/.

Обязательное поле: email,
Обязательное поле: confirmation_code
POST   http://127.0.0.1/api/v1/auth/token/
Content-Type: application/json

    {
        "email": "<EMAIL>",
        "confirmation_code": "<CONFIRMATION CODE>"
    }

**Автор**

Владимир Рязанов - ryazanov745