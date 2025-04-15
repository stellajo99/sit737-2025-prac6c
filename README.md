# Kubernetes Interaction & Update 

## Docker Image
[https://hub.docker.com/r/stellajo99/sit737-2025-prac5p](https://hub.docker.com/r/stellajo99/sit737-2025-prac5p)

## Kubernetes Setup (Docker Desktop)

1. Open Docker Desktop.
2. Go to Settings > Kubernetes.
3. Check "Enable Kubernetes" and click "Apply & Restart".
4. Wait until the status bar shows "Kubernetes is running".
Using Docker Desktop with Kubernetes enabled.

### File Descriptions
| File / Folder              | Description |
|---------------------------|-------------|
| `deployment.yaml`         | Kubernetes deployment configuration for the Node.js app. Updated with a new image tag for versioning. |
| `service.yaml`            | Exposes the app externally using a NodePort service on port 30080. |
| `Dockerfile`              | Used to build the Docker image. Updated version is tagged and pushed to Docker Hub. |
| `README.md`               | Documentation outlining steps for Kubernetes interaction and application update. |
| `screenshots/`            | Folder containing evidence of interaction and updated deployment. |

## How to Interact and Update the App

### Prerequisites
- Docker Desktop installed with Kubernetes enabled
- kubectl installed and configured to use Docker Desktop's Kubernetes

### Part I – Port Forwarding
1. Check resources:
```bash
kubectl get pods
kubectl get services
```
2. Forward local port 8080 to Kubernetes service:
```bash
kubectl port-forward service/prac5p-service 8080:80
```
3. Open your browser and go to:
```
http://localhost:8080
```

### Part II – Application Update
1. Modify your Node.js app code (e.g., change UI message or output text).
2. Rebuild and tag the Docker image:
```bash
docker build -t stellajo99/sit737-2025-prac5p:v2 .
docker push stellajo99/sit737-2025-prac5p:v2
```
3. Update `deployment.yaml` to use the new image:
```yaml
image: stellajo99/sit737-2025-prac5p:v2
```
4. Apply the updated deployment:
```bash
kubectl apply -f deployment.yaml
```
5. Check rollout status:
```bash
kubectl rollout status deployment prac5p-deployment
```
6. Access the updated app:
```
http://localhost:8080
```


## Notes
- The Node.js image has been updated and versioned (e.g., `v2`).
- Port-forwarding was used to interact with the Kubernetes service.
- No cloud resources used—local Kubernetes cluster (Docker Desktop) only.
