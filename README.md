# Demo Project – Flask + Docker + Helm + CI/CD

## Overview
This project demonstrates a complete DevOps workflow including:  
- Python Flask application  
- Containerization with Docker  
- Kubernetes deployment using Helm  
- Continuous Integration and Deployment (CI/CD) with GitHub Actions  
- Git workflow for collaborative development  

The goal is to provide a complete environment where developers can build, run, and deploy the application automatically.

## Project Structure
```
project_demo/
├─ app/                 # Flask application code
│  ├─ main.py
│  └─ Dockerfile
├─ demo-chart/          # Helm chart for Kubernetes deployment
│  ├─ Chart.yaml
│  ├─ templates/
│  └─ values-demo.yaml
├─ .github/workflows/   # GitHub Actions workflow
│  └─ ci-cd.yml
├─ README.md
└─ screenshots/         # Optional: screenshots for documentation
```

## Getting Started

### Prerequisites
- Python 3.x
- Docker
- Git
- (Optional) Kubernetes cluster for Helm deployment

### Local Setup

1. Clone the repository:
```bash
git clone https://github.com/doragayev/demo_project.git
cd project_demo/app
```

2. Build Docker image:
```bash
docker build -t demo-app .
```

3. Run the application:
```bash
docker run -p 5001:5001 demo-app
```

4. Open browser at http://localhost:5001 to see the app running.

## Helm Deployment (CD)

> Note: Helm deployment requires a Kubernetes cluster

1. Install or upgrade the chart:
```bash
helm upgrade --install demo-release ./demo-chart -f ./demo-chart/values-demo.yaml
```
2. Check running pods:
```bash
kubectl get pods
```

3. Forward port to access the service locally:
```bash
kubectl port-forward svc/demo-release 5001:5001
```


## CI/CD Workflow

- Triggered automatically on every push to `main` branch.  

### Continuous Integration (CI) Steps:
1. Checkout code from GitHub
2. Build Docker image from `app/`
3. Push Docker image to Docker Hub

### Continuous Deployment (CD) Steps (if Helm is active):
1. Deploy application to Kubernetes cluster using Helm
2. Update existing deployment if necessary

> Note: In this project, CI builds and pushes Docker images automatically.  
> CD can be enabled to deploy to Kubernetes using Helm.


## Git Workflow

1. Pull latest changes from main branch:
```bash
git pull origin main
```

2. Make changes to main.py or other files.

3. Run and test locally (using Docker or Helm if needed).

4. Stage and commit changes:
```bash
git add .
git commit -m "Your commit message"
```
5. Push changes to GitHub:
```bash
git push origin main
```
>Note: Every push triggers the CI/CD workflow automatically.


## Docker Hub

- Docker image is pushed automatically via CI/CD:
```bash
docker pull doragayev/demo-app:latest
```

To run the image locally:
```bash
docker run -p 5001:5001 doragayev/demo-app:latest
```


## Notes

- You can use `values-demo.yaml` to modify Helm deployment settings such as:
  - Number of replicas
  - Docker image tag
  - Service ports

- CI/CD workflow can be extended to include:
  - Automated tests
  - Linters
  - Notifications

- For local testing, Docker provides an isolated environment to avoid conflicts with your system Python or dependencies.

- Always pull the lates
