# PipeCD v1 Examples

This directory contains examples for PipeCD v1 (plugin-architecture piped) using the `.pipe.yaml` configuration format.

## Key Differences from PipeCD v2

### Configuration Format
- **v1**: Uses `.pipe.yaml` files
- **v2**: Uses `app.pipecd.yaml` files

### API Version
- **v1**: `apiVersion: pipecd.dev/v1beta1`
- **v2**: `apiVersion: pipecd.dev/v1beta1` (same, but different configuration structure)

### Configuration Structure
- **v1**: Simpler configuration structure with direct spec fields
- **v2**: More structured with explicit input/output sections and enhanced pipeline definitions

## Examples

| Name | Description | Deployment Strategy |
|------|-------------|-------------------|
| [kubernetes-quicksync](./kubernetes-quicksync) | Basic Kubernetes deployment with quick sync | Quick Sync |
| [kubernetes-canary](./kubernetes-canary) | Kubernetes deployment with canary strategy | Canary |
| [kubernetes-bluegreen](./kubernetes-bluegreen) | Kubernetes deployment with blue-green strategy | Blue-Green |
| [kubernetes-analysis](./kubernetes-analysis) | Kubernetes deployment with automated analysis | Analysis |
| [kubernetes-approval](./kubernetes-approval) | Kubernetes deployment requiring manual approval | Manual Approval |

## Configuration Reference

### Basic Structure (.pipe.yaml)
```yaml
apiVersion: pipecd.dev/v1beta1
kind: KubernetesApp
spec:
  name: app-name
  labels:
    env: example
    team: platform
  input:
    namespace: default
    # Additional input configurations
  pipeline:
    stages:
      # Pipeline stages (optional)
```

### Available Pipeline Stages (v1)
- `K8S_CANARY_ROLLOUT`: Deploy canary version
- `K8S_CANARY_CLEAN`: Clean up canary resources
- `K8S_PRIMARY_ROLLOUT`: Deploy to primary/production
- `K8S_BLUE_GREEN_ROLLOUT`: Blue-green deployment
- `WAIT_APPROVAL`: Manual approval gate
- `ANALYSIS`: Automated analysis stage

## Usage

These examples are designed to work with PipeCD v1 installations. To use them:

1. Ensure you have a PipeCD v1 piped agent installed
2. Configure your piped to watch this repository
3. Each example directory contains the necessary Kubernetes manifests and `.pipe.yaml` configuration
4. Deploy by committing changes to your Git repository

## Migration Notes

When migrating from v1 to v2:
- Rename `.pipe.yaml` to `app.pipecd.yaml`
- Update configuration structure to use `input` sections
- Review pipeline stage definitions for any syntax changes
- Update API references if using advanced features