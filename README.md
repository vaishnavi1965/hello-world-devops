# Hello World DevOps CI/CD Project

A simple end-to-end DevOps project that demonstrates how to build and deploy a containerized web application using **GitHub, Jenkins, Docker, Docker Hub, and Kubernetes**.

## 🚀 Project Overview

This project automates the deployment of a simple Hello World web application.

### CI/CD Flow

```text
Developer
   |
   v
GitHub
   |
   v
Jenkins
   |
   +----> Build Docker Image
   |
   +----> Push Image to Docker Hub
   |
   v
Kubernetes
   |
   v
Kubernetes Service
   |
   v
Hello World Application
```

## 🛠️ Technologies Used

* **Git & GitHub** – Source code management
* **Jenkins** – CI/CD automation
* **Docker** – Containerization
* **Docker Hub** – Docker image registry
* **Kubernetes** – Container orchestration
* **Docker Desktop Kubernetes** – Local Kubernetes cluster
* **Nginx** – Web server

## 📁 Project Structure

```text
hello-world-devops/
│
├── app/
│   └── index.html
│
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
│
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## 🔄 Jenkins Pipeline Stages

The Jenkins pipeline contains the following stages:

### 1. Git Pull

Jenkins pulls the latest source code from the GitHub repository.

### 2. Build Docker Image

Jenkins builds a Docker image using the Dockerfile.

```bash
docker build -t vaishnavi3008/hello-world:latest .
```

### 3. Push Image to Docker Hub

The Docker image is pushed to Docker Hub.

```bash
docker push vaishnavi3008/hello-world:latest
```

Docker Hub credentials are stored securely in Jenkins Credentials.

### 4. Deploy to Kubernetes

Jenkins deploys the application using Kubernetes YAML manifests.

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

## ☸️ Kubernetes Deployment

The application is deployed with **2 replicas** for basic availability.

```yaml
replicas: 2
```

The application is exposed using a Kubernetes **NodePort** service.

```text
Service Type: NodePort
Port: 80
NodePort: 30080
```

For local testing, Kubernetes port-forwarding can be used:

```bash
kubectl port-forward service/hello-world-service 8081:80
```

Then open:

```text
http://localhost:8081
```

## 🔍 Kubernetes Verification

Check the running pods:

```bash
kubectl get pods
```

Example:

```text
NAME                           READY   STATUS    RESTARTS
hello-world-xxxxxxxxxx-xxxxx  1/1     Running   0
hello-world-xxxxxxxxxx-xxxxx  1/1     Running   0
```

Check the service:

```bash
kubectl get svc
```

Example:

```text
NAME                  TYPE       PORT(S)
hello-world-service   NodePort   80:30080/TCP
```

## 🐳 Docker Verification

Build the image locally:

```bash
docker build -t hello-world:test .
```

Run the container:

```bash
docker run -d --name hello-world-test -p 8081:80 hello-world:test
```

The application can then be accessed at:

```text
http://localhost:8081
```

## 🔐 Jenkins Credentials

Docker Hub credentials are configured in Jenkins using:

```text
Credential ID: dockerhub-credentials
```

Credentials are **not stored directly in the Jenkinsfile**.

##

##
