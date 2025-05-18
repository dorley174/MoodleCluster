# PostgreSQL Deployment for Moodle

This component provides the PostgreSQL backend for Moodle. It includes Kubernetes manifests for deploying a persistent, network-accessible PostgreSQL instance.

## 📦 Contents

- `deployment.yaml`: PostgreSQL Deployment definition
- `service.yaml`: ClusterIP service to expose PostgreSQL to internal services
- `persistent-volume.yaml`: Static Persistent Volume definition
- `pvc.yaml`: Persistent Volume Claim to attach to the PostgreSQL pod

## 🛠 Prerequisites

- Kubernetes cluster (e.g., microk8s or Minikube)
- `kubectl` configured for your cluster
- Storage class support (for dynamic or pre-provisioned PV)
- Docker (for image preparation if needed)

## 🚀 Deployment Steps

1. **Apply the Persistent Volume (optional if dynamic provisioning is used):**

   ```bash
   kubectl apply -f persistent-volume.yaml
   ```
2. **Create the Persistent Volume Claim:**

    ```bash
    kubectl apply -f pvc.yaml
    ```
3. **Deploy PostgreSQL:**

    ```bash
    kubectl apply -f deployment.yaml
    ```
4. **Expose PostgreSQL within the cluster:**

    ```bash
    kubectl apply -f service.yaml
    ```

## 🧪 Testing

After deployment, you can verify the PostgreSQL pod is running:

  ```bash
  kubectl get pods
  ```

And to connect to the database from inside the cluster:

  ```bash
  kubectl run psql-client --image=postgres --rm -it -- \
  psql -h <postgres-service-name> -U <username> -d <database>
  ```
Replace **<em>postgres-service-name</em>**, **<em>username</em>** and **<em>database</em>** with actual values from your manifest.
