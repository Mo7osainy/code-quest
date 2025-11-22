# Voting Application - DevOps Challenge

![Architecture Diagram](./architecture.excalidraw.png)

# Voting Application - DevOps Implementation

## 🚀 Project Overview
A complete DevOps implementation of a distributed voting application with microservices architecture, deployed on Kubernetes using Helm with production-grade security and multi-environment support.

## 🏗️ Architecture
- **Frontend Services**: Vote (Python/Flask) + Result (Node.js)  
- **Backend Services**: Worker (.NET) + Redis + PostgreSQL
- **Two-Tier Networking**: Isolated frontend/backend networks
- **Real-time Results**: WebSocket updates

## 📦 Implementation Status

### ✅ Phase 1 - Containerization & Local Setup
- Docker Compose with two-tier networking
- Health checks for all services
- Frontend ports: 8080 (vote), 8081 (result)

### ✅ Phase 2 - Kubernetes & Helm Deployment  
- Production-grade Helm chart
- Multi-environment support (dev/prod)
- Pod Security Standards (restricted mode)
- Network Policies for database isolation
- Non-root container execution
- Resource limits and probes

### ✅ Phase 3 - Automation & Security
- GitHub Actions CI/CD pipeline
- Security scanning with Trivy
- Multi-environment deployments
- Smoke tests and health checks

## 🛠️ Quick Start

### Prerequisites
- Minikube
- kubectl
- Helm

### Local Deployment (Phase 1)
```bash
# Start minikube cluster
minikube start

# Enable ingress
minikube addons enable ingress

# Build & run all services using Docker Compose
docker compose up --build

# Optional: Populate seed data
docker compose run --rm seed
# Dev Environment
helm install voting-app-dev ./helm-charts -f ./helm-charts/values-dev.yaml

# Prod Environment
helm install voting-app-prod ./helm-charts -f ./helm-charts/values-prod.yaml
# Dev environment
kubectl port-forward svc/vote 32000:80 -n vote-app-dev
kubectl port-forward svc/result 30080:8081 -n vote-app-dev

# Prod environment
kubectl port-forward svc/vote 33000:80 -n vote-app-prod
kubectl port-forward svc/result 33001:8081 -n vote-app-prod
# Dev environment
kubectl port-forward svc/vote 32000:80 -n vote-app-dev
kubectl port-forward svc/result 30080:8081 -n vote-app-dev

# Prod environment
kubectl port-forward svc/vote 33000:80 -n vote-app-prod
kubectl port-forward svc/result 33001:8081 -n vote-app-prod

ssh -i "ssh-key.pem" -L 32000:localhost:32000 ec2-user@<EC2-IP>
ssh -i "ssh-key.pem" -L 32001:localhost:32001 ec2-user@<EC2-IP>


helm install voting-app-dev ./helm-charts -f values-dev.yaml
Namespace: vote-app-dev
Options: "Cats-Dev" vs "Dogs-Dev"
NodePorts: 32001 (vote), 30081 (result)
helm install voting-app-prod ./helm-charts -f values-prod.yaml
Namespace: vote-app-prod
Options: "Cats-Prod" vs "Dogs-Prod"
NodePorts: 32002 (vote), 30082 (result)





