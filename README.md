# api_yamdb / final 
![example workflow](https://github.com/MrGorkiy/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
[![Python](https://img.shields.io/badge/-Python-464646?style=flat&logo=Python&logoColor=ffffff&color=043A6B)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat&logo=Django&logoColor=ffffff&color=043A6B)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat&logo=Django%20REST%20Framework&logoColor=ffffff&color=043A6B)](https://www.django-rest-framework.org/)
[![HTML](https://img.shields.io/badge/-HTML-464646?style=flat&logo=Html5&logoColor=ffffff&color=043A6B)](https://html.spec.whatwg.org/multipage/)
[![CSS](https://img.shields.io/badge/-CSS_Bootstrap-464646?style=flat&logo=Css3&logoColor=ffffff&color=043A6B)]([https://html.spec.whatwg.org/multipage/](https://getbootstrap.ru/))

Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Для приложения настроен Continuous Integration и Continuous Deployment, а это значит, что реализуете:
автоматический запуск тестов,
обновление образов на Docker Hub,
автоматический деплой на боевой сервер при пуше в главную ветку main.


### Быстрый доступ:
- http://mrgorkiy.sytes.net/admin - Панель управления администратора
- http://mrgorkiy.sytes.net/api/v1/ - Api проекта
- http://mrgorkiy.sytes.net/redoc/ - Техническая документация проекта


## Как запустить проект:
- Клонируйте репозиторий `git@github.com:MrGorkiy/yamdb_final.git`
- Скопируйте файлы `docker-compose.yaml` и `nginx/default.conf` из проекта в папке _**infra**_ на сервер в `home/<ваш_username>/docker-compose.yaml` и `home/<ваш_username>/nginx/default.conf` соответственно.
- Установите docker:
    ```bash
    sudo apt install docker.io 
    ```
- Установите docker-compose, с этим вам поможет [официальная документация](https://docs.docker.com/compose/install/).
- Заполните Secrets Actions по шаблону наполнения env переменных в GitHub Actions
    ```
    Наименование:        Содержание:
    DB_ENGINE            django.db.backends.postgresql # указываем, что работаем с postgresql
    DB_NAME              postgres # имя базы данных
    POSTGRES_USER        postgres # логин для подключения к базе данных
    POSTGRES_PASSWORD    postgres # пароль для подключения к БД (установите свой)
    DB_HOST              db # название сервиса (контейнера)
    DB_PORT              5432 # порт для подключения к БД 
    HOST                 194.212.231.123 # ip сервера
    USER                 MrGorkiy # UserName для подключению к серверу
    SSH_KEY              # Приватный ключ доступа для подключению к серверу `cat ~/.ssh/id_rsa`
    PASSPHRASE           # Серкретный ключ\фраза, если ваш ssh-ключ защищён фразой-паролем
    TELEGRAM_TO          # id чата пользователя или чата куда бот будет отправлять результат успешного выполнения
    TELEGRAM_TOKEN       # Токен бота ТГ для отправки уведомления
    DOCKER_USERNAME      # Имя пользователя Docker для публикации образов
    DOCKER_PASSWORD      # Пароль пользоывателя Docker
    ```
- Сделайте коммит в ветку Master/Main и готовый проект развернется у вас на сервере

- На сервере после запуска выполнить миграции:

    ```bash
    docker-compose exec web python manage.py migrate
    ```

- И создать суперпользователя:

    ```bash
    docker-compose exec web python manage.py createsuperuser
    ```

- Заполнение БД в ручную или используя готовое наполнение
    ```bash
    docker-compose exec web python manage.py shell  
    # выполнить в открывшемся терминале:
    >>> from django.contrib.contenttypes.models import ContentType
    >>> ContentType.objects.all().delete()
    >>> quit()
    
    docker-compose exec web python manage.py loaddata fixtures.json
    ```

# Технологии
```
Python, Django, HTTP, HTTPS, Django Rest Framework, PostgreSQL, GitHub Actions, DockerHub
```

# Авторы

Автор: [MrGorkiy](https://github.com/MrGorkiy)

