# KKV-Homelab

A GitOps-managed Kubernetes homelab environment using Flux CD.

## Overview

This repository contains the infrastructure configuration for a Kubernetes homelab environment. It uses [Flux CD](https://fluxcd.io/) to implement GitOps practices, automatically syncing the state of the cluster with the declarations in this repository.

## Repository Structure

```
clusters/
└── dev/
    ├── apps/
    │   ├── cert-manager/
    │   ├── minio/
    │   ├── nginx/
    │   └── vault/
    ├── flux-system/
    └── helm-repositories.yaml
```

## Environments

Currently, the repository contains configuration for the following environments:

- **dev**: Development environment for testing and staging

## Applications

The homelab currently includes the following applications:

- **cert-manager**: Automated TLS certificate management
- **vault**: Secret management and encryption
- **nginx**: Ingress controller
- **minio**: S3-compatible object storage

## Getting Started

### Prerequisites

- Kubernetes cluster
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Flux CD CLI](https://fluxcd.io/docs/installation/)

### Bootstrap Flux

To bootstrap Flux CD on your cluster:

```bash
flux bootstrap github \
  --owner=<your-github-username> \
  --repository=kkv-homelab \
  --branch=main \
  --path=clusters/dev \
  --personal
```

### Sync Status

You can check the sync status of your Flux resources:

```bash
flux get all
```

## Adding New Applications

To add a new application to the homelab:

1. Create a new directory in the `clusters/dev/apps/` folder
2. Add your Kubernetes manifests or Helm release configuration
3. Commit and push to the repository
4. Flux will automatically detect the changes and apply them to the cluster

## Architecture

This homelab follows GitOps principles using Flux CD:

- **Git as the single source of truth**: All configuration is stored in this repository
- **Declarative**: The desired state of the cluster is declared in the repository
- **Automated**: Changes to the repository are automatically applied to the cluster
- **Self-healing**: The system continuously reconciles the actual state with the desired state

## License

[MIT](LICENSE)
