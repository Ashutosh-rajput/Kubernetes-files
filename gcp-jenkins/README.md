# GCP Jenkins Kubernetes Deployment

This directory contains GKE-specific configurations for deploying Jenkins on Google Kubernetes Engine. These manifests leverage GCP-specific features like Workload Identity for secure cloud access.
Please do not use in other environment.

## 🛠️ Configuration Files

```text
gcp-jenkins/
├── jenkins.yaml                   # Main Jenkins StatefulSet with persistent storage
├── jenkins-service-account.yaml   # GCP IAM Service Account
├── jenkins-clusterrole.yaml       # Kubernetes RBAC permissions
└── jenkins-clusterrole-binding.yaml # Binds SA to ClusterRole