# Kubernetes Platform Structure

This repository follows industry best practices for separating platform infrastructure from applications.

## Structure

```
├── platform/                    # Platform team responsibility
│   └── ingress/                 # Ingress controller infrastructure
│       ├── base/                # Base HAProxy manifests
│       └── overlays/            # Environment-specific ingress configs
├── applications/                # Application team responsibility
│   └── hello-world/            # Hello World application
│       ├── base/               # Base application manifests  
│       └── overlays/           # Environment-specific app configs
└── scripts/                    # Deployment automation
```

## Team Responsibilities

### Platform Team
- **Manages**: `platform/` directory
- **Responsible for**: Ingress controllers, monitoring, security, cluster-wide services
- **Deploys**: `kubectl apply -k platform/ingress/base`

### Application Team  
- **Manages**: `applications/` directory
- **Responsible for**: Application deployments, services, configmaps
- **Deploys**: `kubectl apply -k applications/hello-world/overlays/development`

## Deployment Commands

### Infrastructure (Platform Team)
```bash
# Deploy ingress controller
kubectl apply -k platform/ingress/base
```

### Applications (Application Team)
```bash
# Deploy to development
kubectl apply -k applications/hello-world/overlays/development

# Deploy to production  
kubectl apply -k applications/hello-world/overlays/production
```

## Benefits of This Structure

✅ **Clear separation of concerns**: Infrastructure vs application code  
✅ **Team boundaries**: Different teams can own different parts  
✅ **Independent deployments**: Infrastructure and apps deploy separately  
✅ **Scalable**: Easy to add new applications or infrastructure components  
✅ **Industry standard**: Follows professional Kubernetes organization patterns
