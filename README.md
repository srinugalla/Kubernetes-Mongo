# Kubernetes-Mongo 🐳📦

[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)](https://kubernetes.io/) 
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/) 
[![Mongo Express](https://img.shields.io/badge/MongoExpress-000000?logo=mongodb&logoColor=white)](https://github.com/mongo-express/mongo-express)

A **Kubernetes project** to deploy **MongoDB** and **Mongo Express** using Kubernetes manifests.  
Ideal for learning **Secrets**, **ConfigMaps**, **Deployments**, and **Services** in Kubernetes.

---

## 🚀 Overview

This project deploys:

- **MongoDB**: Database backend  
- **Mongo Express**: Web UI for MongoDB  
- **Secrets**: Manage credentials securely  
- **ConfigMaps**: Store configuration  
- **Services**: Expose pods internally and externally  

Tested locally with **Minikube**, can run on any Kubernetes cluster.

---

## 📂 Project Structure

Kubernetes-Mongo/
├─ mongo.yaml # MongoDB Deployment & Service
├─ mongo-secret.yaml # Kubernetes Secret for MongoDB credentials
├─ mongo-configmap.yaml # ConfigMap for Mongo Express
├─ mongo-express.yaml # Mongo Express Deployment
├─ mongo-express-svc.yaml # Mongo Express Service
└─ README.md # This file


---

## 🛠 Prerequisites

- Kubernetes cluster (Minikube for local development)
- kubectl installed
- Docker

---

## ⚡ Setup Instructions

### 1️⃣ Create MongoDB Secret

Generate base64 encoded credentials:

```bash
echo -n 'username' | base64
echo -n 'password' | base64
```
Apply the secret:

```
kubectl apply -f mongo-secret.yaml
```
---

### 2️⃣ Apply ConfigMap
```
kubectl apply -f mongo-configmap.yaml
```
---

### 3️⃣ Deploy MongoDB
```
kubectl apply -f mongo.yaml
```
Check the pod status:
```
kubectl get pods
```
---

### 4️⃣ Deploy Mongo Express
```
kubectl apply -f mongo-express.yaml
kubectl apply -f mongo-express-svc.yaml
```
---

### 🌐 Access Mongo Express

Use Minikube to open the service:
```
minikube service mongodb-express-service
```
- Opens browser at: http://<minikube-ip>:<port>
- Default credentials: username & password from mongodb-secret.yaml
🔑 Make sure to update the secret values for production

---

### 🔍 Verify Deployment
```
kubectl get all
kubectl logs -l app=mongo-express
```
---

### 🔐 Security Notes
- Never commit real credentials
- Base64 encoding is not encryption
- Use proper secret management for production deployments

---

### 🎓 Learnings

- Kubernetes DNS & service discovery
- Secrets vs ConfigMaps
- Pod-to-pod communication
- Exposing services with LoadBalancer & NodePort

---

### ✅ Status

- Working locally on Minikube
- Beginner-friendly example
- Ready for learning and experimentation

---

### 📖 References

- [Kubernetes Docs](https://kubernetes.io/docs/)
- [MongoDB Docs](https://www.mongodb.com/docs/)
- [Mongo Express GitHub](https://github.com/mongo-express/mongo-express)

