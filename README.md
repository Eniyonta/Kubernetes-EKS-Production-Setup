# Kubernetes (EKS) Production Setup

A production-style Kubernetes deployment on AWS EKS with 
autoscaling, ingress, and full monitoring via Prometheus and Grafana.

## Architecture
User → NGINX Ingress → Flask App (EKS Pods) → HPA (autoscaling)
↑
Prometheus + Grafana (monitoring)

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| AWS EKS | Managed Kubernetes cluster |
| Terraform | Infrastructure as Code |
| kubectl | Kubernetes CLI |
| Helm | Kubernetes package manager |
| NGINX Ingress | External traffic routing |
| HPA | Automatic pod scaling |
| Prometheus | Metrics collection |
| Grafana | Monitoring dashboards |

## 🚀 How to Deploy

### 1. Create EKS cluster
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### 2. Connect kubectl
```bash
aws eks update-kubeconfig --region us-east-1 --name flask-eks-cluster
kubectl get nodes
```

### 3. Deploy app
```bash
kubectl apply -f k8s/
```

### 4. Install NGINX Ingress
```bash
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

### 5. Install Monitoring
```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace monitoring --create-namespace -f monitoring/values.yaml
```
