# Kubernetes Manifests Repository

This repository contains Kubernetes configuration files for all my projects. Each project is organized in its own directory with deployment manifests, service definitions, and environment-specific configurations.

## 📁 Repository Structure

```text
├── projects/                   # Main projects directory
│   ├── WealthManager/          # Project 1 
│   │   ├── expense-deployment.yaml
│   │   ├── frontend-deployment.yaml
│   │   ├── mongodb-deployment.yaml
│   │   ├── nexus-deployment.yaml
│   │   ├── userinfo-deployment.yaml
│   │   └── README.md           
│   └── ...                     
│
├── common/                     # Shared resources
│   ├── jenkins-deployment.yaml
│   ├── kafka-deployment.yaml
│   ├── redis-deployment.yaml
│   ├── zookeeper-deployment.yaml
│   └── README.md               
│
├── gcp-jenkins/                # Jenkins setup specific to GCP 
│   ├── jenkins-clusterrole-binding.yaml
│   ├── jenkins-clusterrole.yaml
│   ├── jenkins-service-account.yaml
│   ├── jenkins.yaml
│   ├── jenkinsfile.txt
│   └── README.md
│
├── README.md                   
└── tree.log                    
