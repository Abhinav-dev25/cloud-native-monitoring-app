# 🚀 Cloud Native Resource Monitoring Python App on Kubernetes

> 👨‍💻 Designed & Implemented by **Abhinav Pokhariyal**  
> A complete Cloud-Native Monitoring Application built using Python, Docker, AWS ECR, and AWS EKS.

---

## 📌 Project Overview

This project demonstrates how to build and deploy a **production-style cloud-native monitoring application** using modern DevOps and Cloud technologies.

The application monitors:

- CPU Usage
- Memory Usage
- System Statistics Visualization

It follows a real-world deployment workflow:

```
Flask App → Docker → AWS ECR → AWS EKS → Kubernetes Deployment → Service Exposure
```

---

## 🧠 What I Learned From This Project

1. Building monitoring applications using **Flask + psutil**
2. Running Python applications locally
3. Writing optimized Dockerfiles
4. Building and running Docker containers
5. Creating AWS ECR repositories using **Boto3**
6. Pushing Docker images securely to ECR
7. Creating and managing EKS clusters
8. Automating Kubernetes Deployments & Services using Python
9. Exposing services using Kubernetes port-forward

---

## 🛠️ Tech Stack

- Python 3
- Flask
- psutil
- Plotly
- Docker
- AWS ECR
- AWS EKS
- Kubernetes
- Boto3
- Kubernetes Python Client

---

## 📦 Prerequisites

Make sure the following are installed:

- ✅ AWS Account
- ✅ AWS CLI configured with programmatic access
- ✅ Python 3
- ✅ Docker
- ✅ kubectl
- ✅ VS Code (or any code editor)

---

# ✨ Project Setup Guide

---

# 🔹 Part 1: Running the Flask App Locally

### Step 1: Clone the Repository

```bash
git clone https://github.com/Abhinav-dev25/cloud-native-monitoring-app.git
cd cloud-native-monitoring-app
```

---

### Step 2: Install Dependencies

```bash
pip3 install -r requirements.txt
```

---

### Step 3: Run the Application

```bash
python3 app.py
```

Access the application at:

```
http://localhost:5000
```

---

# 🐳 Part 2: Dockerizing the Application

---

## Step 1: Create Dockerfile

Create a file named `Dockerfile` in the root directory:

```dockerfile
FROM python:3.9-slim-buster

WORKDIR /app

COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

COPY . .

ENV FLASK_RUN_HOST=0.0.0.0

EXPOSE 5000

CMD ["flask", "run"]
```

---

## Step 2: Build Docker Image

```bash
docker build -t cloud-native-monitoring-app .
```

---

## Step 3: Run Docker Container

```bash
docker run -p 5000:5000 cloud-native-monitoring-app
```

Open:

```
http://localhost:5000
```

---

# ☁️ Part 3: Push Docker Image to AWS ECR

---

## Step 1: Create ECR Repository Using Python

```python
import boto3

ecr_client = boto3.client('ecr')

repository_name = 'cloud-native-monitoring-app'
response = ecr_client.create_repository(repositoryName=repository_name)

print(response['repository']['repositoryUri'])
```

---

## Step 2: Authenticate Docker with ECR

```bash
aws ecr get-login-password --region <region> \
| docker login --username AWS \
--password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
```

---

## Step 3: Tag & Push Image

```bash
docker tag cloud-native-monitoring-app:latest <your-ecr-uri>:latest
docker push <your-ecr-uri>:latest
```

---

# ☸️ Part 4: Deploying to AWS EKS Using Python

---

## Step 1: Create EKS Cluster & Node Group

Create:

- EKS Cluster
- Managed Node Group

Update kubeconfig:

```bash
aws eks update-kubeconfig --region <region> --name <cluster-name>
```

---

## Step 2: Create Kubernetes Deployment & Service

Run:

```bash
python3 eks.py
```

> ⚠️ Important: Update the image URI inside `eks.py` before running.

---

## Verify Deployment

```bash
kubectl get deployments
kubectl get services
kubectl get pods
```

---

## Expose the Application

```bash
kubectl port-forward service/my-flask-service 5000:5000
```

Access:

```
http://localhost:5000
```

---

# 🏗️ Architecture Flow

```
Flask Monitoring App
        ↓
Docker Container
        ↓
AWS ECR
        ↓
AWS EKS Cluster
        ↓
Kubernetes Deployment
        ↓
Kubernetes Service
        ↓
Port Forward / LoadBalancer
```

---

# 💡 DevOps & Cloud Concepts Demonstrated

- Containerization
- Cloud Image Registry
- Kubernetes Workloads
- Infrastructure Automation
- Cluster-based Deployment
- Service Networking
- Production-style Cloud Workflow

---

# 🚀 Future Enhancements

- Integrate Prometheus for metrics scraping
- Add Grafana dashboards
- Implement Horizontal Pod Autoscaling
- Add CI/CD Pipeline (GitHub Actions)
- Use LoadBalancer instead of port-forward
- Package deployment using Helm

---

# 👨‍💻 Author

**Abhinav Pokhariyal**  
Cloud & DevOps Enthusiast  
Kubernetes | AWS | Docker | Python  

GitHub: https://github.com/Abhinav-dev25

---
