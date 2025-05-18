# 📚 Moodle Cluster: High Availability & Scalable LMS Deployment

This repository contains the complete setup for deploying a **highly available**, **scalable**, and **observable** Moodle LMS using **Kubernetes (MicroK8s)**, **Docker**, and a monitoring stack built with **Prometheus** and **Grafana**.

## 🎯 Project Objectives

- Deploy Moodle in a Kubernetes cluster with PHP + Nginx
- Use PostgreSQL as the persistent backend database
- Ensure data durability and service discovery
- Monitor application and node-level metrics using Prometheus + Grafana

## 🛠️ Technologies Used

| Component           | Technology       |
|---------------------|------------------|
| Cluster Management  | MicroK8s (Kubernetes) |
| Containerization    | Docker           |
| Database            | PostgreSQL       |
| Web Application     | Moodle (PHP + Nginx) |
| Monitoring - Metrics| Prometheus       |
| Monitoring - Dashboards | Grafana     |
| Node Metrics        | Node Exporter (as DaemonSet) |
| OS                  | Ubuntu           |

## 👨‍💻 Team Members

| Name               | Email                            | GitHub                            | Group |
|--------------------|----------------------------------|------------------------------------|--------|
| Danil Valiev       | d.valiev@innopolis.university    | [dorley174](https://github.com/dorley174) | SD-02 |
| Vyacheslav Molchanov | v.molchanov@innopolis.university | [ub3rch](https://github.com/ub3rch) | SD-02 |
| Aidar Sarvartdinov | a.sarvartdinov@innopolis.university | [AidarSarvartdinov](https://github.com/AidarSarvartdinov) | SD-02 |
| Bulat Gazizov      | b.gazizov@innopolis.university   | [BulatGazizov-dev](https://github.com/BulatGazizov-dev) | SD-02 |

## 📐 Project Structure

The project is organized around modular Kubernetes deployments, with each service or technology housed in its own folder and, where needed, its own Git branch.

- `postgres/` – PostgreSQL manifests (PVC, Deployment, Service)
- `moodle/` – Dockerfile and deployment manifests for Moodle LMS (PHP + Nginx)
- `monitoring/` – Prometheus, Grafana, and Node Exporter setup
- `README.md` – Root documentation (this file)

## 📊 Monitoring Stack

- Prometheus scrapes metrics from:
  - Node Exporter (hardware metrics)
  - Kubernetes pods
- Grafana uses Prometheus as a data source and provides dashboards to visualize:
  - Pod CPU/memory
  - Node health
  - System load under user traffic

## 🔁 Load Testing

Simulated concurrent users were used to validate:
- Pod stability
- Resource monitoring
- Cluster resilience

## 💡 Skills Gained

- Kubernetes: deployments, volumes, services, manifests
- Docker: multi-layer images with PHP and Nginx
- Prometheus + Grafana configuration
- Infrastructure as Code (IaC)
- Collaborative DevOps using Git and modular branches

## 📎 Repository Links

- 📁 [Main GitHub Repository](https://github.com/dorley174/MoodleCluster)
- 📺 [Demo Video (YouTube)](https://youtu.be/wKH-UPujTms)
- 📥 [Demo Video (Google Drive)](https://drive.google.com/file/d/1psxoi8EsNZcpNi4akzlLYsshowyJSU1X/view?usp=sharing)

## 🗂️ Additional Configuration Branches

Each major component has its own branch in this repository with a dedicated `README.md` describing setup and usage in detail:

- [`moodle` branch](https://github.com/dorley174/MoodleCluster/tree/moodle) – Setup of Moodle (Docker + Kubernetes)
- [`postgres` branch](https://github.com/dorley174/MoodleCluster/tree/postgres) – PostgreSQL deployment
- [`monitoring` branch](https://github.com/dorley174/MoodleCluster/tree/monitoring) – Prometheus, Grafana, Node Exporter configuration

---
