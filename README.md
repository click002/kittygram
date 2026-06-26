# Kittygram Final Project

![Main Kittygram Workflow](https://github.com/click002/kittygram_final/actions/workflows/main.yml/badge.svg)

Проект для публикации фотографий котов с возможностью создания постов, добавления изображений и авторизации пользователей.

## Стек технологий
- **Backend:** Python 3.12, Django 5.1, Django REST Framework
- **Frontend:** React
- **Database:** PostgreSQL
- **Web Server:** Gunicorn, Nginx
- **DevOps:** Docker, Docker Compose, GitHub Actions (CI/CD)

## Как развернуть проект

### Локальная разработка (без Docker)

1. Клонируйте репозиторий и перейдите в него:
   ```bash
   git clone https://github.com/click002/kittygram_final.git
   cd kittygram_final
   ```

2. Создайте и активируйте виртуальное окружение:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Для Windows: venv\Scripts\activate
   ```

3. Установите зависимости из файла `requirements.txt`:
   ```bash
   pip install -r backend/requirements.txt
   ```

4. Создайте файл `.env` в корне проекта по образцу `.env.example` и заполните его (см. раздел [Настройки окружения](#настройки-окружения)).

5. Примените миграции и создайте суперпользователя для доступа в админку:
   ```bash
   python backend/manage.py migrate
   python backend/manage.py createsuperuser
   ```

6. Запустите сервер разработки:
   ```bash
   python backend/manage.py runserver
   ```
   Проект будет доступен по адресу: http://127.0.0.1:8000/

### Запуск в Docker (Production)

1. Убедитесь, что файл `.env` заполнен и находится в корне проекта.

2. Соберите и запустите контейнеры в фоновом режиме:
   ```bash
   docker compose -f docker-compose.production.yml up -d
   ```

3. Примените миграции внутри контейнера `backend`:
   ```bash
   docker compose -f docker-compose.production.yml exec backend python manage.py migrate
   ```

4. Создайте суперпользователя (по желанию):
   ```bash
   docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser
   ```

5. Соберите статические файлы:
   ```bash
   docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic --no-input
   ```

Проект будет доступен по адресу: http://localhost:9000/

## Настройки окружения
Для работы приложения необходимо создать файл `.env` со следующими переменными:

```env
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
POSTGRES_DB=kittygram
DB_HOST=db
DB_PORT=5432
DJANGO_SECRET_KEY=your-secret-key
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1,ваш-домен
```

## Автор
Никита Филин ([click002](https://github.com/click002))
