# ☸️ Kubernetes Day 02 - Hands-On

---

# Objective

In this hands-on, we will:

- Enable Kubernetes in Docker Desktop
- Verify the Kubernetes Cluster
- Create our first Deployment
- Observe Deployment → ReplicaSet → Pods hierarchy
- Understand how Kubernetes creates resources automatically
- Troubleshoot common errors

---

# Prerequisites

- Docker Desktop Installed
- Kubernetes Enabled
- kubectl Installed
- WSL2 Enabled (Windows)

---

# Step 1 - Enable Kubernetes

Docker Desktop

↓

Settings

↓

Kubernetes

↓

Enable Kubernetes

↓

Click Apply

Wait until Kubernetes Cluster becomes Ready.

---

# Step 2 - Verify Cluster

Command

```bash
kubectl cluster-info
```

Purpose

Checks whether Kubernetes Control Plane is running.

Expected Output

```
Kubernetes control plane is running at ...
CoreDNS is running at ...
```

---

# Step 3 - Verify Worker Node

Command

```bash
kubectl get nodes
```

Purpose

Displays all Worker Nodes available in the cluster.

Expected Output

```
NAME               STATUS   ROLES           VERSION

docker-desktop     Ready    control-plane   v1.xx.x
```

---

# Step 4 - Create Deployment YAML

File

```
deployment.yaml
```

Content

```yaml
apiVersion: apps/v1

kind: Deployment

metadata:
  name: urbanx-backend

spec:
  replicas: 3

  selector:
    matchLabels:
      app: backend

  template:
    metadata:
      labels:
        app: backend

    spec:
      containers:
      - name: backend
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

# Step 5 - Deploy Application

Command

```bash
kubectl apply -f deployment.yaml
```

Purpose

Creates Deployment inside Kubernetes.

Expected Output

```
deployment.apps/urbanx-backend created
```

---

# Step 6 - Verify Deployment

Command

```bash
kubectl get deployments
```

Purpose

Shows Deployment status.

---

# Step 7 - Verify ReplicaSet

Command

```bash
kubectl get replicasets
```

Purpose

Shows ReplicaSet created automatically by Deployment.

---

# Step 8 - Verify Pods

Command

```bash
kubectl get pods
```

Purpose

Displays Pods created by ReplicaSet.

Expected Output

```
NAME

urbanx-backend-xxxxx

urbanx-backend-yyyyy

urbanx-backend-zzzzz
```

---

# Step 9 - Describe Deployment

Command

```bash
kubectl describe deployment urbanx-backend
```

Purpose

Displays complete Deployment information.

---

# Step 10 - Delete Deployment

Command

```bash
kubectl delete deployment urbanx-backend
```

Purpose

Deletes Deployment along with ReplicaSet and Pods.

---

# Resource Creation Flow

Developer

↓

kubectl apply

↓

API Server

↓

Deployment

↓

ReplicaSet

↓

Pods

↓

Containers

---

Explain what happens internally when you execute kubectl apply -f deployment.yaml ?

Developer executes kubectl apply.

↓

The API Server validates the manifest.

↓

The desired state is stored in etcd.

↓

A Deployment object is created.

↓

The Deployment creates a ReplicaSet.

↓

The ReplicaSet creates the required Pods.

↓

The Scheduler selects an appropriate Worker Node.

↓

The Kubelet on that node communicates with the container runtime.

↓

The container image is pulled.

↓

Containers start.

↓

Pods become Ready.

↓

The API Server updates the cluster state.

-----------------------------------------------------

# Common Errors

## Error 1

```
Unable to connect to localhost:8080
```

Reason

- Kubernetes Cluster not running
- API Server unavailable
- Current Context not configured

Solution

- Enable Kubernetes in Docker Desktop
- Wait until cluster becomes Ready
- Verify using:

```bash
kubectl cluster-info
```

---

## Error 2

```
current-context is not set
```

Reason

No Kubernetes Cluster configured.

Solution

Enable Kubernetes and wait until Docker Desktop creates the cluster.

---

## Error 3

ImagePullBackOff

Reason

Container image not found.

Solution

Verify image name.

Example

```
nginx:latest
```

---

# Today's Learning

✔ Kubernetes Cluster

✔ Deployment

✔ ReplicaSet

✔ Pods

✔ kubectl apply

✔ Troubleshooting
