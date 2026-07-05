# ☸️ Kubernetes Day 01 - Hands-On

---

# Objective

The objective of today's hands-on is to:

- Install Kubernetes locally
- Install kubectl
- Install Minikube
- Start a Kubernetes Cluster
- Verify the Cluster
- Understand basic kubectl commands

---

# Environment

Operating System

- Windows 11

Editor

- VS Code

Terminal

- Git Bash

Container Platform

- Docker Desktop

Kubernetes Tool

- Minikube

CLI Tool

- kubectl

---

# Why Do We Need Minikube?

In production, Kubernetes runs on multiple servers.

However, during learning we cannot purchase multiple servers.

Minikube creates a single-node Kubernetes Cluster on our local machine.

Think of it as a mini Kubernetes environment for learning and testing.

---

# Step 1 - Verify Docker

Check whether Docker Desktop is running.

Command

```bash
docker ps
```

Expected Output

```text
CONTAINER ID

IMAGE

STATUS
```

If Docker is running successfully, continue.

---

# Step 2 - Verify kubectl

Command

```bash
kubectl version --client
```

Purpose

Checks whether kubectl is installed.

Expected Output

```text
Client Version:
```

---

# Step 3 - Verify Minikube

Command

```bash
minikube version
```

Purpose

Checks whether Minikube is installed.

Expected Output

```text
minikube version:
```

---

# Step 4 - Start Kubernetes Cluster

Command

```bash
minikube start
```

Purpose

Creates a local Kubernetes Cluster.

What Happens Internally?

- Creates Control Plane
- Creates Worker Node
- Starts Kubernetes Components
- Configures kubectl
- Cluster becomes Ready

---

# Step 5 - Verify Cluster

Command

```bash
kubectl cluster-info
```

Purpose

Displays the Kubernetes Control Plane information.

Expected Output

```text
Kubernetes control plane is running...
```

---

# Step 6 - Check Worker Nodes

Command

```bash
kubectl get nodes
```

Purpose

Displays all Worker Nodes available in the Cluster.

Expected Output

```text
NAME       STATUS

minikube   Ready
```

Meaning

Ready means the Worker Node is healthy and capable of running Pods.

---

# Step 7 - Check Namespaces

Command

```bash
kubectl get namespaces
```

Purpose

Displays the default namespaces available in Kubernetes.

Expected Output

```text
default

kube-system

kube-public

kube-node-lease
```

---

# Step 8 - Check Pods

Command

```bash
kubectl get pods -A
```

Purpose

Displays Pods running in all namespaces.

Explanation

-A

means

All Namespaces

Expected Output

Multiple Kubernetes system Pods.

---

# Step 9 - Get Cluster Information

Command

```bash
kubectl get all -A
```

Purpose

Displays most Kubernetes resources from all namespaces.

Useful during troubleshooting.

---

# Step 10 - Stop Cluster

Command

```bash
minikube stop
```

Purpose

Stops the Kubernetes Cluster without deleting it.

---

# Step 11 - Start Cluster Again

Command

```bash
minikube start
```

Purpose

Starts the existing Kubernetes Cluster.

---

# Step 12 - Delete Cluster

Command

```bash
minikube delete
```

Purpose

Deletes the entire local Kubernetes Cluster.

Use only when required.

---

# Useful kubectl Commands

Check Nodes

```bash
kubectl get nodes
```

Check Pods

```bash
kubectl get pods
```

Check Pods in All Namespaces

```bash
kubectl get pods -A
```

Check Services

```bash
kubectl get svc
```

Check Deployments

```bash
kubectl get deployments
```

Check Namespaces

```bash
kubectl get namespaces
```

Cluster Information

```bash
kubectl cluster-info
```

---

# Common Errors

## Error

```text
The connection to the server localhost:8080 was refused
```

Reason

Kubernetes Cluster is not running.

Solution

```bash
minikube start
```

---

## Error

```text
kubectl command not found
```

Reason

kubectl is not installed.

---

## Error

```text
Docker is not running
```

Reason

Docker Desktop is stopped.

Solution

Start Docker Desktop.

---

# Interview Scenario

Interviewer

"How do you verify whether your Kubernetes Cluster is healthy?"

Answer

I usually verify:

```bash
kubectl cluster-info
```

Then

```bash
kubectl get nodes
```

Finally

```bash
kubectl get pods -A
```

to ensure the Control Plane, Worker Node, and Kubernetes system Pods are running correctly.

---

# Best Practices

✅ Ensure Docker Desktop is running before starting Minikube.

✅ Verify the cluster after every restart.

✅ Learn kubectl commands before deploying applications.

✅ Use kubectl get pods -A for troubleshooting.

---

# Hands-On Summary

Today we performed:

✅ Verified Docker

✅ Verified kubectl

✅ Verified Minikube

✅ Started Kubernetes Cluster

✅ Verified Cluster

✅ Checked Worker Nodes

✅ Checked Namespaces

✅ Checked Pods

✅ Learned essential kubectl commands

This completes the practical setup required before deploying applications in Kubernetes.
