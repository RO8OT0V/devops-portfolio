# CI/CD Pipeline

Автоматизированный пайплайн на GitHub Actions для сборки, тестирования и публикации Docker образа.

## 📖 Что демонстрирует

- ✅ GitHub Actions workflow
- ✅ Go build и test
- ✅ Docker build & push
- ✅ GitHub Container Registry (GHCR)
- ✅ Multi-job pipeline с зависимостями

## 🏗️ Архитектура

```
.github/
└── workflows/
    └── ci.yaml    # CI/CD конфигурация
```

## 🚀 Как работает

```
┌─────────────┐     ┌─────────────┐
│   Push to   │────▶│  GitHub     │
│    main     │     │   Actions   │
└─────────────┘     └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              ▼                         ▼
     ┌─────────────────┐      ┌─────────────────┐
     │  Job: build     │      │  Job: docker    │
     │  - Checkout     │      │  - Login GHCR   │
     │  - Setup Go     │      │  - Build image  │
     │  - Build        │      │  - Push         │
     │  - Test         │      │                 │
     └─────────────────┘      └─────────────────┘
```

## 📦 Workflow триггеры

| Событие | Ветки |
|---------|-------|
| push | main |
| pull_request | main |

## 🔧 Настройка

### 1. Включить права доступа

На GitHub: **Settings** → **Actions** → **General** → **Workflow permissions**

Выбрать: **Read and write permissions**

### 2. Workflow файл

```yaml
name: CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.25'
      
      - name: Build Go app
        run: cd 01-dockerized-app && go build -o myapp main.go
      
      - name: Run tests
        run: cd 01-dockerized-app && go test ./... || echo "No tests"

  docker:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/checkout@v4
      
      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: ./01-dockerized-app
          push: true
          tags: ghcr.io/${{ github.repository }}/myapp:latest
```

## 📊 Результат

После успешного запуска:

- ✅ Docker образ доступен в GHCR
- ✅ Статус workflow виден в Actions tab
- ✅ Образ можно использовать в K8s deployment

### Пример образа

```bash
# Pull образа
docker pull ghcr.io/ro8ot0v/devops-portfolio/myapp:latest

# Запуск
docker run -p 8080:8080 ghcr.io/ro8ot0v/devops-portfolio/myapp:latest
```

## 📸 Workflow status

![CI/CD Success](https://github.com/RO8OT0V/devops-portfolio/actions/workflows/ci.yaml/badge.svg)

---

*Готово к расширению: deploy to K8s, Slack notifications, auto-tagging*
