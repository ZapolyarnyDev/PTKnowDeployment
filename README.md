# PTKnow Deploy

Репозиторий для развёртывания и общей документации проекта PTKnow.

## Быстрый запуск

1. Создать `.env` на основе `.env.example`.
2. Заполнить секреты и адреса.
3. Запустить:

```bash
docker compose up -d
```

4. Проверить логи backend:

```bash
docker compose logs -f backend
```

## Что поднимается

- `postgres` - база данных PostgreSQL
- `backend` - PTKnow Server из Docker-образа

## Примечание

`compose.yaml` и `.env.example` - это шаблон для локального и серверного развёртывания через переменные окружения
