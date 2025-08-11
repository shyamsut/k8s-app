# 🚀 Kubernetes Local Cluster with Minikube

## 📌 Project Overview
This project demonstrates **Kubernetes application deployment and management** using **Minikube** on a local environment.  
It covers the complete workflow of:
- Cluster setup
- Application deployment
- Service exposure
- Scaling
- Monitoring & debugging

This project is part of my **DevOps Internship** at **Delvex Innovation Private Limited (Jaipur)**.

---

## 🛠️ Tools & Technologies
- **Kubernetes** (Minikube)
- **kubectl** CLI
- **Docker**
- **YAML** configuration files
- **Nginx** (sample application)

---

## 🎯 Objectives
- Build a local Kubernetes cluster using Minikube
- Deploy a sample application using Deployment manifest
- Expose the app with NodePort Service
- Scale the application pods
- Monitor and debug the running workloads

---

## 📂 Project Structure
.
├── deploy.yaml # Kubernetes deployment for Nginx app
├── service.yaml # NodePort service configuration
├── screenshots/ # Screenshots of pods, services & browser output
└── README.md # Project documentation

---

## ⚙️ Step-by-Step Implementation

### **1️⃣ Install & Start Minikube**

# Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start the cluster
minikube start --driver=docker
2️⃣ Install kubectl

sudo snap install kubectl --classic
kubectl version --client
3️⃣ Create Deployment
deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
  labels:
    app: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp-container
          image: nginx:latest
          ports:
            - containerPort: 80
Apply:

kubectl apply -f deployment.yaml
4️⃣ Create NodePort Service
service.yaml

apiVersion: v1
kind: Service
metadata:
  name: app-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
Apply:

kubectl apply -f service.yaml
5️⃣ Verify Deployments

kubectl get pods
kubectl get svc
kubectl get all 
https://github.com/shyamsut/k8s-app/blob/main/deploy-service-scale.png


6️⃣ Access the Application

minikube ip
Open in browser:


http://<minikube-ip>:30007


7️⃣ Scale the Application

kubectl scale deployment app-deployment --replicas=4
kubectl get pods


8️⃣ Debugging & Logs

kubectl describe pod <pod-name>
kubectl logs <pod-name>
📊 Key Learnings
How to set up Kubernetes locally with Minikube

Writing and applying YAML manifests

Exposing applications using NodePort

Scaling and monitoring Kubernetes workloads

Using kubectl for debugging

📌 Author
Shyam Suthar

