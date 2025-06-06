# Kubernetes Manifests Repository

This repository contains Kubernetes configuration files for all my projects. Each project is organized in its own directory with deployment manifests, service definitions, and environment-specific configurations.

## 📁 Repository Structure

```text
├── projects/                   # Main projects directory
│   ├── <project-1>/            # Project 1
│   │   ├── base/               # Base manifests (common across environments)
│   │   │   ├── deployment.yaml
│   │   │   ├── service.yaml
│   │   │   └── configmap.yaml
│   │   ├── overlays/           # Environment-specific configurations
│   │   │   ├── development/
│   │   │   ├── staging/
│   │   │   └── production/
│   │   └── README.md           # Project-specific documentation
│   │
│   ├── <project-2>/            # Project 2
│   └── ...
│
├── common/                     # Shared resources
│   ├── ingress/                # Ingress configurations
│   ├── cert-manager/           # SSL certificate setups
│   └── monitoring/             # Monitoring resources
│
├── tools/                      # Helper scripts/tools
├── .github/                    # CI/CD workflows (GitHub Actions)
├── README.md                   # This file
└── .kubeconfig-example         # Example kubeconfig (gitignored)