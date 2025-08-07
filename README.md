# Kubernetes Drupal Learning Project

## Architecture
- Development: POP OS (local kind cluster + FreeLens)
- Production: Ubuntu 22.04 @ 192.168.40.25 (k3s)
- GUI: FreeLens (installed via flatpak)

## Workflow
1. Develop and test locally with kind
2. Commit manifests to git  
3. Deploy to production server via kubectl

## Network
- Internal network: 192.168.40.0/24
- Production server: 192.168.40.25
