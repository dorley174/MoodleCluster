
# Moodle Docker Image and Kubernetes Configurations

## Requirements
- **Docker**: For building docker image of Moodle.
- **Kubernetes Cluster**: To deploy and manage your Moodle application.

## Installation Guide
### Step 1: Build the Docker Image

Navigate to the image directory:

```bash
cd image
```

Edit the `config.php` file if you want to use your own PostgreSQL instance. Then, build the Docker image:

```bash
docker build -t <your-image-name> .
```

Push the image to your preferred container registry:

```bash
docker push <your-image-name>
```

### Step 2. Deploy to Kubernetes

Next, move to the Kubernetes configuration directory:

```bash
cd ../k8s
```

#### Step 2.1: Create Persistent Volume

To ensure Moodle data is saved and not lost after restarts, create a Persistent Volume:

```bash
kubectl apply -f persistent-volume.yaml
kubectl apply -f pvc.yaml
```

#### Step 2.2: Create a Service for Moodle

Create a Service for your Moodle application. The default configuration is a NodePort Service, but you can change it to ClusterIP by modifying the service type in `service.yaml`:

```bash
kubectl apply -f service.yaml
```

#### Step 2.3: Deploy the Moodle Container

Deploy your Moodle container using the deployment configuration:

```bash
kubectl apply -f deployment.yaml
```

**Important Note**: Make sure to specify the name of your Docker image in `deployment.yaml`.

### Step 3: Expose the Service

For production environments, expose the service to the internet and implement load balancing if you have multiple Moodle instances. We recommend using an Ingress controller:

```bash
kubectl apply -f ingress.yaml
```
