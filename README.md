# Hello World DevOps CI/CD Project

A simple end-to-end DevOps project that demonstrates how to build and deploy a containerized web application using **GitHub, Jenkins, SonarQube, Docker, Docker Hub, and Kubernetes**.

## 🚀 Project Overview

This project automates the deployment of a simple Hello World web application.

### CI/CD Flow

```text
Developer
   |
   v
GitHub
   |
   | GitHub Webhook
   v
Jenkins
   |
   +----> SonarQube Analysis
   |
   +----> Build Docker Image
   |
   +----> Tag Image with Jenkins Build Number
   |
   +----> Push Image to Docker Hub
   |
   v
Kubernetes
   |
   +----> Deployment
   |
   +----> Kubernetes Service
   |
   v
Hello World Application
