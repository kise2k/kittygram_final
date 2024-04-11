Проект KITTYGRAM

Учебный проект: Коты

Описание проекта: Проект позволяет выложить фото своего питомца и посмотреть фото чужих. Можно добавить цвет, имя, и достижения пушистого друга.

Стэк технологий:
  [Python 3.9](https://www.python.org/downloads/)
  [Django 3.2.3](https://www.djangoproject.com/download/)
  [djangorestframework 3.12.4](https://pypi.org/project/djangorestframework/#files)

Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:
    git@github.com:kise2k/kittygram_final.git
    cd kittygram_final

Установить виртуальное окружение и зависимости
    python -m venv venv
    source venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r backend/requirements.txt

В корне проекта создайте файл .env и пропишите в него свои данные.

Пример:
    POSTGRES_DB=kittygram
    POSTGRES_USER=kittygram_user
    POSTGRES_PASSWORD=kittygram_password
    DB_NAME=kittygram
    DB_HOST=имя хоста базы данных
    DB_PORT=порт базы данных
    SECRET_KEY=your-secret-key
    DEBUG=False
    ALLOWED_HOSTS=ip,local_ip,localhost,domen

Установите [docker](https://www.docker.com/) на свой компьютер.

Запустите проект через docker compose:

    docker compose -f docker-compose.production.yml up --build -d

Выполнить миграции:

    docker compose -f docker-compose.yml exec backend python manage.py migrate

Соберите статику и скопируйте ее:

    docker compose -f docker-compose.yml exec backend python manage.py collectstatic
    docker compose -f docker-compose.yml exec backend cp -r /app/static_backend/. /backend_static/static/

Workflow

Для использования CI и CD: в репозитории GitHub Actions `Settings/Secrets/Actions` прописать Secrets - переменные окружения для доступа к сервисам:

    DOCKER_USERNAME                # имя пользователя DockerHub
    DOCKER_PASSWORD                # пароль от DockerHub
    HOST                           # ip хоста
    USER                           # имя пользователя
    SSH_KEY                        # приватный ssh-ключ
    PASSPHRASE                     # пароль от SSH
    TELEGRAM_TO                    # id бота в телеграм
    TELEGRAM_TOKEN                 # api key телеграм-бота

Срабатывает при пуше в любую ветку и автоматически отрабатывает данные действия:
    tests - Проверка по PEP8 и запуск pytest. Дальнейшие шаги только для ветки main!
    build_and_push_to_docker_hub - сборка и поставка образов на DockerHub.
    deploy - запуск проекта на сервер посредством копирования образов из аккаунта на DockerHub.
    send_message - отправка уведомления в Telegram.

Автор:

Седякин Кирилл

https://github.com/kise2k
