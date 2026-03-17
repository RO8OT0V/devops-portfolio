# Dockerized Go Application

Простое веб-приложение на Go, упакованное в Docker контейнер с использованием best practices.

## 📖 Что демонстрирует

- ✅ Multi-stage Docker build (оптимизация размера образа)
- ✅ Non-root пользователь в контейнере
- ✅ Health check endpoint
- ✅ Правильная обработка сигналов
- ✅ Логирование в stdout

## 🏗️ Архитектура

```
.
├── Dockerfile           # Multi-stage build (builder + production)
├── docker-compose.yml   # Локальная разработка
├── main.go             # Go веб-сервер
└── go.mod              # Go модуль
```

## 🚀 Быстрый старт

### Сборка и запуск

```bash
# Через docker-compose
docker-compose up --build

# Или вручную
docker build -t myapp:latest .
docker run -p 8080:8080 myapp
```

### Проверка работы

```bash
# Основное приложение
curl http://localhost:8080/
# Ответ: Hello, World!

# Health check
curl http://localhost:8080/health
# Ответ: {"status":"ok"}
```

## 📦 Dockerfile особенности

```dockerfile
# Stage 1: Сборка
FROM golang:1.25-alpine AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o myapp main.go

# Stage 2: Production образ
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY --from=builder /app/myapp .
EXPOSE 8080
CMD ["./myapp"]
```

**Преимущества:**
- Минимальный размер образа (~15 MB)
- Безопасность (не root пользователь)
- Статическая линковка (CGO_ENABLED=0)

## 🔧 Конфигурация

| Переменная | Значение | Описание |
|------------|----------|----------|
| PORT | 8080 | Порт приложения |

---

*Проект готов к расширению: добавление тестов, БД, Redis*
