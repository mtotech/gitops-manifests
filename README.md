# Production Grade GitOps Manifests Repository
### ArgoCD Kubernetes Helm Prometheus GitOps
________________________________________
## Overview
### This repository serves as the GitOps source of truth for a Production Grade Kubernetes Platform running on Amazon EKS.
### All Kubernetes deployments, environment configurations, monitoring configurations, and platform resources are managed declaratively through Git and synchronized automatically using ArgoCD.
________________________________________
## GitOps Architecture
Developer

    │
    
    ▼
    
GitHub (gitops-manifests)
    │
    ▼
ArgoCD
    │
    ▼
Amazon EKS
    │
 ┌──┼───────────────┐
 ▼  ▼               ▼

Dev  Staging      Prod

    │
    ▼

Monitoring Stack

(Prometheus + Node Exporter + kube-state-metrics)
________________________________________
Repository Structure
gitops-manifests/

├── applications/
│   ├── root-app.yaml
│   ├── dev.yaml
│   ├── staging.yaml
│   └── prod.yaml
│
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
│
├── quotas/
│   ├── dev-quota.yaml
│   ├── staging-quota.yaml
│   └── prod-quota.yaml
│
├── monitoring/
│   ├── monitoring-app.yaml
│   ├── prometheus-values.yaml
│   └── grafana-values.yaml
│
└── docs/
________________________________________
Implemented Phases
Phase	Description	Status
Phase 07	ArgoCD GitOps	✅
Phase 08	Multi Environment Strategy	✅
Phase 09	Monitoring Foundation	✅
Phase 11	AWS Load Balancer Controller	🚧 Planned
Phase 12	Alerting & Notifications	🚧 Planned
________________________________________
ArgoCD App of Apps Pattern
The platform uses the App of Apps pattern for centralized management.
root-app
│
├── gitops-dev
├── gitops-staging
└── gitops-prod
Benefits:
•	Centralized Control
•	Environment Isolation
•	Easier Scaling
•	GitOps Best Practices
________________________________________
Multi Environment Strategy
Namespaces:
dev
staging
prod
Each environment has:
•	Independent Deployment
•	Independent Configuration
•	Independent Resource Limits
•	Environment-Specific Values
________________________________________
Resource Governance
Implemented:
dev-quota
staging-quota
prod-quota
Controls:
•	CPU Requests
•	CPU Limits
•	Memory Requests
•	Memory Limits
________________________________________
Monitoring Foundation
Monitoring components deployed using GitOps:
Prometheus Operator
Provides:
•	Metrics Collection
•	Service Discovery
•	Kubernetes Monitoring
Node Exporter
Provides:
•	CPU Metrics
•	Memory Metrics
•	Filesystem Metrics
•	Network Metrics
kube-state-metrics
Provides:
•	Deployment Metrics
•	Pod Metrics
•	ReplicaSet Metrics
•	Namespace Metrics
________________________________________
Validation Commands
ArgoCD Applications
kubectl get applications -n argocd
Namespaces
kubectl get ns
Pods
kubectl get pods -A
Resource Quotas
kubectl get resourcequota -A
Monitoring Stack
kubectl get pods -n monitoring
________________________________________
Screenshots
ArgoCD Applications
screenshots/phase7-argocd.png
Namespaces
screenshots/phase8-namespaces.png
Multi Environment Pods
screenshots/phase8-pods.png
Resource Quotas
screenshots/resource-quotas.png
Monitoring Stack
screenshots/phase9-monitoring.png
________________________________________
GitOps Workflow
Git Commit
    │
    ▼
Git Push
    │
    ▼
ArgoCD Detects Change
    │
    ▼
Sync
    │
    ▼
Amazon EKS Updated
________________________________________
Resume Highlights
•	Implemented GitOps deployment strategy using ArgoCD.
•	Designed App of Apps architecture for Kubernetes platform management.
•	Built multi-environment deployment model using Dev, Staging and Production namespaces.
•	Implemented namespace resource governance using ResourceQuotas.
•	Deployed Prometheus-based Kubernetes monitoring through GitOps workflows.
•	Managed Kubernetes platform operations using declarative manifests.
________________________________________
Planned Enhancements
Phase 11
AWS Load Balancer Controller
•	IRSA
•	OIDC Integration
•	ALB Ingress
•	External Access
Phase 12
Alerting & Notifications
•	AlertManager
•	Grafana Alerts
•	Slack Integration
•	Deployment Alerts
•	Infrastructure Alerts
Future
Centralized Logging
•	Loki
•	Promtail
•	LogQL
•	Grafana Log Dashboards
________________________________________
Author
Neeraj Kumar
AWS Certified Solutions Architect – Associate
HashiCorp Certified Terraform Associate
Cloud & DevOps Engineer
________________________________________
Project Status
GitOps Platform Status: Production Ready
Current Completion: ~90%
GitHub Portfolio Ready: ✅
Resume Ready: ✅
Interview Ready: ✅
