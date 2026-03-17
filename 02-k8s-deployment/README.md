# Kubernetes Deployment

Развёртывание Go приложения в Kubernetes кластере с использованием best practices.

## 📖 Что демонстрирует

- ✅ Deployment с 3 репликами
- ✅ Liveness и Readiness probes
- ✅ Resource limits и requests
- ✅ Service (NodePort)
- ✅ Labels и selectors

## 🏗️ Архитектура

```
.
├── deployment.yaml    # Deployment конфигурация
└── service.yaml       # Service конфигурация
```

## 🚀 Быстрый старт

### Развёртывание в кластере

```bash
# Применить манифесты
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Проверить статус
kubectl get pods -l app=myapp
kubectl get svc myapp

# Посмотреть логи
kubectl logs -l app=myapp
```

### Удаление

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

## 📦 Конфигурация

### Deployment

| Параметр | Значение | Описание |
|----------|----------|----------|
| replicas | 3 | Количество подов |
| image | myapp:latest | Docker образ |
| containerPort | 8080 | Порт приложения |

### Resources

| Тип | CPU | Memory |
|-----|-----|--------|
| requests | 100m | 64Mi |
| limits | 200m | 128Mi |

### Probes

| Тип | Path | Port | Initial Delay | Period |
|-----|------|------|---------------|--------|
| liveness | /health | 8080 | 5s | 10s |
| readiness | /health | 8080 | 5s | 5s |

### Service

| Параметр | Значение |
|----------|----------|
| type | NodePort |
| port | 8080 |
| nodePort | 30080 |

## 🔍 Проверка работы

```bash
# Получить IP ноды
kubectl get nodes -o wide

# Доступ к приложению
curl http://<NODE_IP>:30080/
curl http://<NODE_IP>:30080/health
```

## 📊 Манифесты

### Deployment highlights

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "64Mi"
  limits:
    cpu: "200m"
    memory: "128Mi"

livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

---

*Готово к расширению: Ingress, HPA, ConfigMaps, Secrets*
