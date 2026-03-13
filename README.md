# Trend React Application – DevOps Deployment

## Project Overview

This project demonstrates a **production-style DevOps pipeline** for deploying a React application.
The application is containerized using Docker, built and deployed automatically using Jenkins CI/CD, and deployed to Kubernetes with a LoadBalancer service.

The pipeline integrates **GitHub, Jenkins, DockerHub, and Kubernetes** to automate the application lifecycle.

---

# Architecture

Developer → GitHub → Jenkins CI/CD → DockerHub → Kubernetes Cluster → LoadBalancer → Users

---

# Technologies Used

* React (Frontend application)
* Docker (Containerization)
* Jenkins (CI/CD automation)
* GitHub (Version control)
* DockerHub (Container registry)
* Kubernetes (Container orchestration)
* AWS EC2 (Jenkins server)

---

# Repository Structure

```
Trend/
│
├── dist/                 # Built React application
├── Dockerfile            # Docker image configuration
├── Jenkinsfile           # Jenkins CI/CD pipeline
├── deployment.yaml       # Kubernetes deployment
├── service.yaml          # Kubernetes LoadBalancer service
└── README.md
```

---

# Step 1 – Clone the Repository

```bash
git clone https://github.com/Junaid-dot-max/Trend.git
cd Trend
```

---

# Step 2 – Dockerize the Application

## Dockerfile

```
FROM nginx:alpine
COPY dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Build Docker Image

```
docker build -t <dockerhub-username>/trend-react-app:latest .
```

Run Container

```
docker run -p 3000:80 <dockerhub-username>/trend-react-app
```

Application will run at:

```
http://localhost:3000
```

---

# Step 3 – Push Docker Image to DockerHub

Login to DockerHub

```
docker login
```

Push image

```
docker push <dockerhub-username>/trend-react-app:latest
```

---

# Step 4 – Jenkins CI/CD Pipeline

Jenkins automates:

1. Pull latest code from GitHub
2. Build Docker image
3. Push image to DockerHub
4. Deploy application to Kubernetes

## Jenkinsfile

Pipeline stages:

```
Checkout
Build Image
Push Image
Deploy to Kubernetes
```

---

# Step 5 – Kubernetes Deployment

## deployment.yaml

Creates a deployment with 2 replicas of the application.

```
kubectl apply -f deployment.yaml
```

---

## service.yaml

Exposes the application using a Kubernetes LoadBalancer.

```
kubectl apply -f service.yaml
```

---

# Step 6 – Access the Application

Get service external IP:

```
kubectl get svc
```

Example output:

```
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP
trend-service   LoadBalancer   10.100.xx.xx     34.xx.xx.xx
```

Open in browser:

```
http://<EXTERNAL-IP>
```

---

# CI/CD Pipeline Flow

1. Developer pushes code to GitHub
2. Jenkins pipeline is triggered
3. Jenkins builds Docker image
4. Image pushed to DockerHub
5. Kubernetes deployment updated
6. Application becomes available via LoadBalancer

---

# Jenkins Plugins Used

* Git
* Docker Pipeline
* Kubernetes
* Pipeline
* Blue Ocean

---

# Security

* DockerHub authentication via Jenkins credentials
* SSH key authentication used for EC2 access

---

# Monitoring (Optional Enhancement)

Prometheus and Grafana can be integrated with Kubernetes to monitor:

* Pod health
* CPU usage
* Memory usage
* Application uptime

---

# Outcome

✔ React application containerized using Docker
✔ CI/CD pipeline implemented with Jenkins
✔ Docker images stored in DockerHub
✔ Application deployed to Kubernetes
✔ LoadBalancer exposes the application to users

---

# Author

Junaid Ahamed
DevOps Deployment Project
