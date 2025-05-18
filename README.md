# Monitoring with Prometheus and Grafana in the MoodleCluster Project

This project contains configurations for monitoring a Kubernetes cluster using Prometheus and Grafana.

---

## What's included

- **Node Exporter** — DaemonSet to collect metrics from each node in the cluster.
- **Prometheus** — collects and stores metrics from node-exporter and other sources.
- **Grafana** — visualizes metrics from Prometheus using dashboards.

---

## How to run

1. Apply the node-exporter DaemonSet to collect node metrics:

```bash
kubectl apply -f k8s/node-exporter/daemonset.yml
```

2. Create a ConfigMap with Prometheus configuration:

```bash
kubectl apply -f k8s/monitoring/prometheus-config.yaml
```

3. Deploy Prometheus:

```bash
kubectl apply -f k8s/monitoring/prometheus-deployment.yaml
kubectl apply -f k8s/monitoring/prometheus-service.yaml
```

4. Deploy Grafana (assumed to be already deployed and accessible).

## Useful commands

1. View pods and services in the monitoring namespace:

```bash
kubectl get pods -n monitoring
kubectl get svc -n monitoring
```

2. Port-forward for local access to Prometheus:

```bash
kubectl port-forward -n monitoring svc/prometheus-service 9090:9090
```

3. Port-forward for local access to Grafana (if Grafana is deployed in the same namespace):

```bash
kubectl port-forward -n monitoring svc/grafana 3000:3000
```


## Grafana setup

1. Open Grafana at: http://localhost:3000

2. Default login/password: admin / admin (change after first login).

3. Add Prometheus as a data source:

4. URL: http://prometheus-service.monitoring.svc.cluster.local:9090

5. Import a ready-made dashboard for node-exporter or create your own.
