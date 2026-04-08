# PTKnow Deploy

Репозиторий предназначен для развёртывания проекта и хранения общей документации по его запуску

## 📦 Что находится в репозитории

- `compose.yaml` — базовый файл для запуска frontend, backend и PostgreSQL
- `compose.dev.yaml` — локальное расширение для разработки с MinIO
- `.env.example` — шаблон переменных окружения

## 🚀 Базовый запуск

1. Создать `.env` на основе `.env.example`.
2. Заполнить секреты и параметры окружения.
3. Запустить сервисы:

```bash
docker compose up -d
```

4. Проверить логи серверной части:

```bash
docker compose logs -f backend
```

В базовом режиме поднимаются:
- `frontend`
- `postgres`
- `backend`

## 🧪 Локальный режим разработки с MinIO

Если нужно проверить работу с S3-совместимым хранилищем локально, следует использовать оба файла Compose:

```bash
docker compose -f compose.yaml -f compose.dev.yaml up -d
```

В этом режиме дополнительно поднимаются:
- `minio`
- `minio-init`

`minio-init` автоматически создаёт бакет, указанный в `APP_FILE_S3_BUCKET`.

Основные адреса:
- frontend: `http://localhost`
- MinIO API: `http://localhost:9000`
- MinIO Console: `http://localhost:9001`

## 🛠️ Полезные команды

Базовый запуск:

```bash
docker compose up -d
```

Запуск с MinIO:

```bash
docker compose -f compose.yaml -f compose.dev.yaml up -d
```

Остановка:

```bash
docker compose down
```

Остановка режима с MinIO:

```bash
docker compose -f compose.yaml -f compose.dev.yaml down
```

Остановка с удалением данных:

```bash
docker compose -f compose.yaml -f compose.dev.yaml down -v
```

Логи на бэкенде:

```bash
docker compose logs -f backend
```

Логи на фронтенде:

```bash
docker compose logs -f frontend
```

Логи MinIO:

```bash
docker compose -f compose.yaml -f compose.dev.yaml logs -f minio
```

## 📎 Примечание

Базовый `compose.yaml` публикует наружу только `frontend`.
`backend` доступен только внутри docker-сети и должен вызываться через `/api` на фронтовом `nginx`
Базовый `compose.yaml` не зависит от локального MinIO и подходит как нейтральный шаблон для развёртывания.
Сценарий локальной проверки S3-совместимого хранилища вынесен в `compose.dev.yaml`
