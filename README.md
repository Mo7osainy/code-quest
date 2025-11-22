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

# Optional: Populate seed dataAccess the Application
bash
# Method 1: Port Forwarding
kubectl port-forward svc/vote 32000:80 -n vote-app-dev
kubectl port-forward svc/result 30080:8081 -n vote-app-dev

# Method 2: Ingress (after adding hosts)
echo "$(minikube ip) vote.local.com result.local.com" | sudo tee -a /etc/hosts
URLs
Vote App: http://vote.local.com or http://localhost:32000

Result App: http://result.local.com or http://localhost:30080

🔧 Multi-Environment Setup
Development Environment
bash
helm install voting-app-dev ./voting-app -f values-dev.yaml
Namespace: vote-app-dev

Options: "Cats-Dev" vs "Dogs-Dev"

NodePorts: 32001 (vote), 30081 (result)

Production Environment
bash
helm install voting-app-prod ./voting-app -f values-prod.yaml
Namespace: vote-app-prod

Options: "Cats-Prod" vs "Dogs-Prod"

NodePorts: 32002 (vote), 30082 (result)

🛡️ Security Features
Pod Security: Restricted PSA policies

Network Isolation: Database network policies

Non-root Containers: Run as user 1000

Seccomp Profiles: RuntimeDefault

Capability Drop: All privileges removed

Resource Limits: CPU/Memory constraints

📊 Architecture Details
Services
vote: Python Flask app (port 80)

result: Node.js app (port 4000)

worker: .NET worker service

redis: Message broker (port 6379)

postgres: Database (port 5432)

Networking
Frontend Tier: vote + result (user-facing)

Backend Tier: worker + redis + postgres (internal)

Headless Services: For stateful workloads

🔄 Data Flow
Users vote → Vote service

Votes queued → Redis

Worker processes → Redis to PostgreSQL

Results displayed → Result service via WebSocket

🚨 Troubleshooting
bash
# Check pod status
kubectl get pods -n vote-app-dev

# View logs
kubectl logs -f deployment/vote -n vote-app-dev

# Check services
kubectl get svc -n vote-app-dev

# Debug ingress
kubectl get ingress -n vote-app-dev
📝 Notes
Uses minikube for local Kubernetes development

Headless Services for stateful applications

Network Policies enforce backend isolation

Helm for templating and multi-environment management

Production-ready security configurations

Status: ✅ Fully Implemented - Ready for Production Deployment
docker compose run --rm seed



