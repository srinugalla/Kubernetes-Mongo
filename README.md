## Kubernetes-Mongo

Kubernetes manifests to deploy MongoDB along with a Mongo Express UI on a Kubernetes cluster.

This repo demonstrates how to use Kubernetes Secrets, ConfigMaps, Deployments, and Services to run a database + web admin UI setup.

---

### 🧱 Project Structure
mongo-configmap.yaml    # ConfigMap for app configuration
mongo-express.yaml      # Mongo Express deployment + service
mongo-secret.yaml       # Secret for MongoDB credentials
mongo.yaml              # MongoDB deployment + service
README.md               # This documentation

---

### 🚀 Overview

This setup deploys:

MongoDB — a NoSQL database container

Internal Service — lets other pods (like mongo-express) talk to MongoDB

Secret — stores admin credentials for MongoDB securely

ConfigMap — stores connection info (e.g., DB host name)

Mongo Express — web-based admin interface to view & manage your DB

Environment variables in the pod specs are configured using Secrets and ConfigMaps so sensitive values are not hardcoded.

---

### 🧠 Prerequisites

Make sure you have:

A Kubernetes cluster (Minikube, kind, GKE, etc.)

kubectl installed and configured

(Optional) A LoadBalancer service provider if exposing mongo-express externally

---

### 📦 Deploying the Stack

Apply each resource in the correct order:

1. Create the Secret
kubectl apply -f mongo-secret.yaml


This stores your MongoDB username/password encoded in a Kubernetes Secret.

2. Deploy MongoDB
kubectl apply -f mongo.yaml


This manifest creates:

A Deployment for MongoDB using the official image

A Service (ClusterIP) for internal access

Environment variables taking credentials from the secret created earlier.

3. Add the ConfigMap
kubectl apply -f mongo-configmap.yaml


This file provides configuration like the internal MongoDB service address required by the UI.

4. Deploy Mongo Express
kubectl apply -f mongo-express.yaml


This manifest creates:

A Deployment for Mongo Express

A Service to expose the UI

Environment variables pulled from both the Secret and ConfigMap.

---

### 🧪 Verify

Check pods & services:

kubectl get pods
kubectl get services


Access the Mongo Express UI (if exposed externally):

### Example for Minikube
minikube service mongo-express

---

### 🧩 How It Works

Secrets store sensitive credentials so they’re not visible in plaintext.

ConfigMaps manage non-sensitive config values like service names.

Deployments ensure your containers are running and recover automatically.

Services assign stable network names so pods can talk to one another.

---

### ⚙️ Customization

You can tweak:

Number of replicas

MongoDB version

Storage (add PVCs for durable data)

LoadBalancer types for public access

---

### 🧹 Cleanup

Remove all resources:

kubectl delete -f mongo-express.yaml \
               -f mongo-configmap.yaml \
               -f mongo.yaml \
               -f mongo-secret.yaml

---

### 📚 Learn More

For more comprehensive Kubernetes/MongoDB patterns (Operators, StatefulSets, persistent storage, sharded clusters), you can explore the official MongoDB Kubernetes docs and community tools:
