# Kubernetes learning journey: From concepts to production

**Learning approach**: Start with practical problems, understand components as needed, build production-ready infrastructure through hands-on experience.

## Learning philosophy

This project demonstrates Black Box learning applied to Kubernetes infrastructure:

- Start with real problems instead of theoretical concepts
- Build production systems rather than toy examples  
- Learn components when needed to solve immediate challenges
- Use professional patterns from day one
- Version control everything with Infrastructure as Code

**Background**: 30 years Linux server administration experience, learning Kubernetes for modern infrastructure and cloud migration.

## What you'll find here

This repository contains a complete production-grade Kubernetes platform built through progressive learning. You'll see the evolution from basic concepts to enterprise patterns through practical implementation.

### Major achievements

**Production-grade networking**
- MetalLB LoadBalancer with automatic external IP assignment
- HAProxy Ingress for professional traffic routing
- DNS integration with proper host-based routing
- Standard port access without NodePort complexity

**Enterprise storage patterns**
- NFS implementation for shared storage across pod replicas
- PersistentVolumes with proper Kubernetes abstractions
- Environment-specific storage backends
- Data persistence across pod restarts and scaling

**Multi-container application deployment**
- Drupal 11 CMS with database integration
- nginx + php-fpm container architecture
- External database connectivity
- Shared volumes between containers

**Professional configuration management**
- Environment-specific configuration via ConfigMaps
- Automatic database detection without manual setup
- Separate development and production environments
- Proper credential management and security patterns

**Infrastructure as Code excellence**
- Git-based workflows for all infrastructure changes
- Team separation between platform and application responsibilities
- Environment promotion with same manifests across dev/prod
- Professional deployment patterns

## Repository structure

```
kubernetes-drupal-learning/
├── platform/                          # Platform team responsibility
│   ├── ingress/                       # HAProxy ingress controller
│   │   ├── base/                      # Base configuration
│   │   └── overlays/production/       # LoadBalancer service type
│   └── metallb/                       # MetalLB load balancer
│       ├── base/                      # MetalLB manifests
│       └── overlays/production/       # IP pool configuration
├── applications/                      # Application team responsibility
│   └── hello-world/                  # Multi-application namespace
│       ├── base/                     # Base application manifests
│       │   ├── persistent-volume-claim.yaml
│       │   ├── deployment.yaml       # Static content application
│       │   ├── service.yaml
│       │   ├── ingress.yaml
│       │   ├── nginx-drupal-configmap.yaml
│       │   ├── drupal-database-configmap.yaml
│       │   ├── drupal-deployment.yaml    # nginx + php-fpm containers
│       │   ├── drupal-service.yaml
│       │   └── drupal-ingress.yaml
│       └── overlays/
│           ├── development/          # Local testing environment
│           └── production/           # Production environment
└── README.md
```

## Technologies mastered

**Kubernetes distributions**
- k3s for production deployment (lightweight, single-binary)
- kind for local development and testing

**Networking and load balancing**
- MetalLB for bare metal LoadBalancer implementation
- HAProxy Ingress for production traffic management
- External IP management with automatic assignment

**Storage systems**
- NFS for shared storage across pods
- PersistentVolumes for Kubernetes storage abstractions
- Environment-specific storage backends

**Application platforms**
- Drupal 11 with container-native deployment
- Multi-container application architecture
- External database integration patterns

**Configuration management**
- Kustomize for environment-specific configuration
- ConfigMaps for application configuration injection
- Overlay patterns for environment differences

## Deployment workflows

### Development workflow
```bash
# Edit infrastructure manifests locally
vim applications/hello-world/base/drupal-deployment.yaml

# Test on local cluster
kubectl apply -k applications/hello-world/overlays/development
kubectl port-forward service/drupal-service 8081:80 -n hello-world-dev
```

### Production deployment
```bash
# 1. Commit infrastructure changes
git add .
git commit -m "Add new deployment configuration"
git push origin main

# 2. Deploy to production server
cd ~/kubernetes-drupal-learning
git pull origin main

# 3. Deploy platform infrastructure
kubectl apply -k platform/metallb/overlays/production
kubectl apply -k platform/ingress/overlays/production

# 4. Deploy applications
kubectl apply -k applications/hello-world/overlays/production

# 5. Verify deployment
kubectl get pods -n hello-world-prod
```

## Current status

**Live applications**
- Drupal 11 CMS fully installed and operational
- Static website serving custom content
- External database with separate development and production instances
- NFS shared storage with persistent files across multiple pod replicas

**Infrastructure services**
- MetalLB LoadBalancer with IP pool management
- HAProxy Ingress controller with host-based routing
- NFS server providing shared persistent storage
- External database server for application data

**Operational capabilities**
```bash
# Scale applications
kubectl scale deployment drupal-nginx-php --replicas=5 -n hello-world-prod

# Monitor applications
kubectl logs -f deployment/drupal-nginx-php -c nginx -n hello-world-prod
kubectl top pods -n hello-world-prod
```

## Black box learning outcomes

### Problems solved through hands-on discovery
1. "How do I get external IPs on bare metal?" → Discovered MetalLB
2. "Why can't multiple pods share files?" → Learned storage access modes
3. "How do I manage environment-specific configuration?" → Mastered Kustomize overlays
4. "How do real companies handle database configuration?" → Implemented industry patterns

### Professional patterns learned
- Team separation between platform and application responsibilities
- Infrastructure as Code with Git-based deployment workflows
- Environment promotion using same manifests with different configurations
- Multi-container applications with shared storage
- External integration patterns for databases and storage

### Enterprise skills developed
- Production debugging with container logs and exec access
- Storage management including PV/PVC lifecycle and access modes
- Configuration management with environment-specific injection
- Multi-environment operations with development to production promotion
- Application architecture with multi-container pods and external dependencies

## Next phase: Microservices and event streaming

**Current milestone**: Monolithic Drupal successfully deployed
**Next goal**: Microservices architecture with event streaming
**Planned components**: Authentication service, Kafka event platform, additional microservices

---

## Achievement summary

**Started with**: Basic Kubernetes concepts and simple containers
**Achieved**: Production-ready platform with professional infrastructure patterns  
**Learned**: Real-world Kubernetes administration through practical problem-solving
**Result**: Enterprise-grade foundation ready for microservices expansion

This journey demonstrates that you can master complex infrastructure through practical, problem-driven learning rather than extensive theoretical study.
