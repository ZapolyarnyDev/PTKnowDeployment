# PTKnow Deploy

Репозиторий для развёртывания и общей документации проекта PTKnow.

## Что находится в репозитории

- `compose.yaml` — базовый шаблон развёртывания backend и PostgreSQL
- `compose.dev.yaml` — локальное dev-расширение с MinIO для S3-compatible режима
- `.env.example` — шаблон переменных окружения

## Базовый запуск

1. Создать `.env` на основе `.env.example`.
2. Заполнить секреты и параметры окружения.
3. Запустить:

```bash
docker compose up -d
```

4. Проверить логи backend:

```bash
docker compose logs -f backend
```

Что поднимается:
- `postgres`
- `backend`

## Локальный dev-режим с MinIO

Если нужно протестировать S3-compatible хранилище локально, использовать оба файла Compose:

```bash
docker compose -f compose.yaml -f compose.dev.yaml up -d
```

В этом режиме дополнительно поднимаются:
- `minio`
- `minio-init`

`minio-init` автоматически создаёт bucket, указанный в `APP_FILE_S3_BUCKET`.

Основные адреса dev-режима:
- backend: `http://localhost:8095`
- MinIO API: `http://localhost:9000`
- MinIO Console: `http://localhost:9001`

## Полезные команды

Базовый запуск:

```bash
docker compose up -d
```

Dev-режим с MinIO:

```bash
docker compose -f compose.yaml -f compose.dev.yaml up -d
```

Остановка:

```bash
docker compose down
```

Остановка dev-режима:

```bash
docker compose -f compose.yaml -f compose.dev.yaml down
```

Остановка с удалением данных:

```bash
docker compose -f compose.yaml -f compose.dev.yaml down -v
```

Логи backend:

```bash
docker compose logs -f backend
```

Логи MinIO в dev-режиме:

```bash
docker compose -f compose.yaml -f compose.dev.yaml logs -f minio
```

## Примечание

Базовый `compose.yaml` не привязан к локальному MinIO и подходит как более нейтральный deploy-шаблон.
Локальный S3-compatible сценарий вынесен в `compose.dev.yaml`.
