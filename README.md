# DevOps Portfolio

[![CI/CD](https://github.com/RO8OT0V/devops-portfolio/actions/workflows/ci.yaml/badge.svg)](https://github.com/RO8OT0V/devops-portfolio/actions/workflows/ci.yaml)

Привет! Я начинающий DevOps-инженер. Здесь собраны мои учебные проекты, демонстрирующие навыки в области контейнеризации, оркестрации и CI/CD.

## 📋 Проекты

| # | Проект | Технологии | Статус |
|---|--------|------------|--------|
| 01 | [Dockerized Go Application](./01-dockerized-app/) | Docker, Multi-stage build | ✅ Готов |
| 02 | [Kubernetes Deployment](./02-k8s-deployment/) | K8s, Deployment, Service, Probes | ✅ Готов |
| 03 | [CI/CD Pipeline](./03-cicd-pipeline/) | GitHub Actions, GHCR | ✅ Готов |

---

## 🛠 Навыки

### Containerization
- Docker, Docker Compose
- Multi-stage builds
- Image optimization

### Orchestration
- Kubernetes (Deployment, Service, Ingress)
- Health checks (liveness/readiness probes)
- Resource management

### CI/CD
- GitHub Actions
- Automated testing
- Docker image build & push to GHCR

### Programming
- Go (basic)
- Bash scripting

---

## 📸 CI/CD Pipeline

*Автоматический пайплайн: build → test → docker build → push*

---

## 🚀 Быстрый старт

### Запуск приложения локально

```bash
# Проект 1: Docker
cd 01-dockerized-app
docker-compose up --build

# Проект 2: Kubernetes (нужен кластер)
cd 02-k8s-deployment
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Проверка работы

```bash
# Health check
curl http://localhost:8080/health

# Основное приложение
curl http://localhost:8080/
```

---

## 📬 Контакты

- **GitHub:** [RO8OT0V](https://github.com/RO8OT0V)
- **Email:** ro8otov@mail.ru
- **Telegram:** @robotov

---

*Открыт к предложениям по работе и фриланс-заказам!*
