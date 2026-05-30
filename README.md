# Kittygram

Социальная сеть для любителей кошек. Позволяет регистрироваться, добавлять фото своих питомцев с именем, цветом и годом рождения, а также просматривать записи других пользователей.

## Технологии

- Python 3.11, Django 3.2, Django REST Framework
- PostgreSQL 13
- React (Node.js 18)
- Nginx 1.22
- Docker / Docker Compose
- GitHub Actions (CI/CD)
- Gunicorn

## Быстрый старт (локально)

### 1. Клонируйте репозиторий

```bash
git clone https://github.com/<your-username>/kittygram_final.git
cd kittygram_final
```

### 2. Создайте файл `.env`

Скопируйте пример и заполните значения:

```bash
cp .env.example .env
```

Содержимое `.env`:

```
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=your_password
DB_HOST=db
DB_PORT=5432
SECRET_KEY=your-django-secret-key
DEBUG=False
ALLOWED_HOSTS=localhost 127.0.0.1
```

### 3. Запустите контейнеры

```bash
docker compose up -d --build
```

Приложение будет доступно по адресу: [http://localhost:9000](http://localhost:9000)

Админка Django: [http://localhost:9000/admin/](http://localhost:9000/admin/)

## CI/CD (GitHub Actions)

Workflow в `.github/workflows/main.yml`:

- **При пуше в любую ветку:** линтинг ruff, тесты бэкенда (Python 3.10/3.11/3.12), тесты фронтенда.
- **При пуше в `main`:** сборка образов и публикация на Docker Hub, уведомление в Telegram.

### Необходимые секреты в GitHub

| Секрет | Описание |
|---|---|
| `DOCKER_USERNAME` | Логин на Docker Hub |
| `DOCKER_PASSWORD` | Пароль / токен Docker Hub |
| `TELEGRAM_TO` | ID Telegram-чата для уведомлений |
| `TELEGRAM_TOKEN` | Токен Telegram-бота |

## Структура Docker-образов

| Образ | Контейнер |
|---|---|
| `<username>/kittygram_backend` | `backend` |
| `<username>/kittygram_frontend` | `frontend` |
| `<username>/kittygram_gateway` | `gateway` |
| `postgres:13` | `db` |
