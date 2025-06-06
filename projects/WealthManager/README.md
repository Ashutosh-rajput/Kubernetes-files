# Running WealthManager

This guide provides instructions on how to deploy and run the WealthManager application using Kubernetes.

## Overview

WealthManager is a microservices-based personal finance application. To run it, you will need to deploy several services into a Kubernetes cluster, along with its dependencies: Kafka and Redis. An optional CI/CD pipeline using Jenkins can also be set up.

The core application services are:
*   **`userinfo`**: Manages user accounts, authentication, and authorization.
*   **`expense`**: Handles all other backend APIs related to expenses, earnings, budgets, and subscriptions.
*   **`frontend`**: The ReactJS user interface.
*   **`mongo`**: The MongoDB database instance.
*   **`nexus`**: Handles asynchronous operations like sending emails and document processing.

## Prerequisites
*  Create Namespace `backend`,`frontend`, `database-namespace`,`kafka-namespace`.
*   A running Kubernetes cluster (e.g., Minikube, Kind, Docker Desktop K8s, GKE, EKS, AKS).
*   `kubectl` command-line tool configured to communicate with your cluster.
*   (Optional) Docker installed if you need to build images locally, though this guide assumes pre-built images referenced in Kubernetes manifests.
*   Access to the project repository containing the Kubernetes manifest files.

## Directory Structure (Assumed)
````
wealthmanager/
├── userinfo-deployment.yaml
├── expense-deployment.yaml
├── frontend-deployment.yaml
├── mongo-statefulset.yaml
├── nexus-deployment.yaml
│
├── common/
│ ├── kafka-deployment.yaml
│ ├── zookeeper-deployment.yaml
│ ├── redis-deployment.yaml
│ └── jenkins-deployment.yaml (Use for docker and for Gke use GCP jenkins yamls.)
````
## Deployment Steps

### 1. Deploy External Dependencies (Kafka & Redis)

WealthManager requires Kafka and Redis. You can deploy them in your Kubernetes cluster or use external/managed services.

**Deploy within Kubernetes (if manifests are provided)**

If Kubernetes manifests for Kafka and Redis are available in the `common/kafka/` and `common/redis/` directories:

## 2. Deploy Core Application Services

Apply the Kubernetes manifest files for each WealthManager service. The recommended deployment order is:

1. **Database**
2. **Backend Services**
3. **Frontend**


```bash
kubectl apply -f mongo-deployment.yaml

kubectl apply -f userinfo-deployment.yaml

kubectl apply -f expense-deployment.yaml

kubectl apply -f nexus-deployment.yaml

kubectl apply -f frontend-deployment.yaml
```

You may also apply individual files if needed.

> ⚠️ Ensure the frontend manifest is configured to connect to the API Gateway or backend services (`userinfo`, `expense`) as per your architecture.

---

## 3. Verify Deployments

Check the status of your deployments using:

```bash
kubectl get pods -A
kubectl get services -A
kubectl get deployments -A
```

Check logs for any runtime issues:

```bash
kubectl logs -f <pod-name> -n <namespace-if-any>
```

Ensure all pods are in `Running` state and desired replicas are available.

---

## 4. Accessing the Application

Once the frontend is running, access WealthManager via the service IP or hostname.

### Using a LoadBalancer:
```bash
kubectl get svc frontend-service  # or your actual frontend service name
```
Look for the `EXTERNAL-IP`.
---

## Optional: CI/CD Pipeline with Jenkins

### For GCP Kubernetes (GKE):
- Configure Jenkins for GKE with appropriate credentials.
- Use a provided `Jenkinsfile` for automated build and deployment.
```bash
cd gcp-jenkins/
```

### For Docker-based Jenkins:
```bash
cd common/jenkins/
```


> ⚙️ Ensure Jenkins has access to your Docker registry and Kubernetes credentials.

---

## Important Notes

- **Configuration**: Use `ConfigMaps` and `Secrets` to supply MongoDB, Kafka, and Redis details to your services.
- **Namespace**: Include `-n <your-namespace>` with `kubectl` if deploying to a specific namespace.
- **Private Registries**: Use `imagePullSecrets` in your deployment YAMLs for private Docker images.
- **Persistent Volumes**: Ensure `mongo` has properly configured `PVCs` and `PVs` for data persistence.

---

> 🧠 **Tip**: Always refer to the specific `YAML` files and service documentation for precise configuration and environment-specific settings.

