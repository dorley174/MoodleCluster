# Moodle Kubernetes Cluster Deployment

## 🎯 Цель проекта

Развернуть Moodle-кластер в Kubernetes с высокой доступностью и масштабируемостью, используя microk8s, Prometheus + Grafana для мониторинга и HAProxy для балансировки нагрузки.

---

## 📌 Очередность шагов

1. ✅ Настроить кластер microk8s (доступ, плагины, volumes)
2. ✅ Разработка и деплой PostgreSQL
3. ✅ Сборка Docker-образа для Moodle (PHP + Nginx)
4. ✅ Написание и деплой манифестов для Moodle
5. ✅ Настройка HAProxy/Ingress и проверка доступа
6. ✅ Установка Node Exporter + Prometheus + Grafana
7. ✅ Настройка HPA
8. 🧪 Финальное тестирование, нагрузочное тестирование
9. 📝 Документация в README.md

---

## 🧰 Используемые средства

| Цель                  | Инструмент             |
|-----------------------|------------------------|
| Кластер               | MicroK8s               |
| Контейнеризация       | Docker                 |
| Балансировка нагрузки | HAProxy                |
| Мониторинг            | Prometheus, Grafana    |
| СУБД                  | PostgreSQL             |
| Moodle + сервер       | PHP, Nginx             |
| Автоскейлинг          | HPA (metrics-server)   |
| Контроль версий       | Git + GitHub           |
| Операционная система  | Ubuntu (151.80.47.11)  |

---

## 🔧 Разделение задач

### A. Инфраструктура и кластер

- Проверить/настроить microk8s:
  ```bash
  microk8s status --wait-ready
  microk8s enable dns storage ingress metrics-server helm3
  alias kubectl='microk8s kubectl'
  ```
- Создать PersistentVolumes и StorageClass
- Проверить `kubectl get pods -A`

---

### B. PostgreSQL

- Использовать официальный Docker-образ PostgreSQL
- Написать Deployment + Service + PVC
- Подключение к Moodle через переменные среды:
  - `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`

---

### C. Moodle + PHP + Nginx

- Собрать кастомный Docker-образ:
  - PHP-FPM + расширения
  - Nginx + конфиг
- Примонтировать volume для `/moodledata`
- Deployment, Service, HPA

---

### D. Load Balancing (HAProxy)

- Развернуть HAProxy под с конфигом на несколько Moodle pod’ов
- Вариант: использовать microk8s Ingress

---

### E. Мониторинг (Prometheus + Grafana)

- Node Exporter — DaemonSet
- Prometheus:
  - Helm или вручную
  - ConfigMap с targets или service discovery
- Grafana:
  - Подключить Prometheus как data source
  - Импортировать дашборды

---

### F. Horizontal Pod Autoscaler (HPA)

- Использовать metrics-server
- Написать HPA-манифест на CPU или Memory

---

## 🔐 Конфигурации и секреты

- Использовать Kubernetes Secret и ConfigMap
- Подключение переменных среды через `envFrom`

---

## 🛠 Полезные команды

### Статус кластера:
```bash
microk8s status --wait-ready
```

### Включение нужных аддонов:
```bash
microk8s enable dns storage ingress metrics-server helm3
```

### Проверка подов:
```bash
kubectl get pods -A
```

### Установка Prometheus через Helm:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus
```

---

## ✅ Не забыть

- Открытые порты: HAProxy, Grafana, Moodle (Ingress/NodePort)
- Firewall: открыть нужные порты
- Автоматизация: скрипт `init.sh` для деплоя

---

## 🔄 Возможные улучшения

- Поддержка нескольких нод с автоматическим discovery
- Настройка внешнего хранилища (например, NFS)
- Автоматизация CI/CD (например, GitHub Actions)

---

## 📁 Структура репозитория

```
moodle-cluster/
├── docker/
│   └── moodle-nginx-php/
│       ├── Dockerfile
│       ├── nginx.conf
│       └── php.ini
├── k8s/
│   ├── moodle/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── hpa.yaml
│   ├── postgres/
│   │   ├── deployment.yaml
│   │   └── pvc.yaml
│   ├── haproxy/
│   │   └── deployment.yaml
│   ├── prometheus/
│   │   ├── configmap.yaml
│   │   └── deployment.yaml
│   ├── grafana/
│   │   └── deployment.yaml
│   └── node-exporter/
│       └── daemonset.yaml
├── scripts/
│   └── init.sh
└── README.md
```
