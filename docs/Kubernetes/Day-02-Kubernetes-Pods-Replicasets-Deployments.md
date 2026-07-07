# ☸️ Kubernetes Day 02 - Pods, ReplicaSets & Deployments

---

# Learning Objectives

By the end of Day 02, you will understand:

- What is a Pod
- Why Kubernetes uses Pods instead of Containers
- Pod Architecture
- Single Container vs Multi-Container Pods
- What is a ReplicaSet
- Why ReplicaSets were introduced
- Difference between Pod and ReplicaSet
- What is a Deployment
- Deployment vs ReplicaSet
- Rolling Updates
- Labels & Selectors
- Deployment YAML
- Internal Working of Deployment

---

# Revision from Day 01

Yesterday we learned the Kubernetes Architecture.

Developer

↓

API Server

↓

etcd

↓

Controller Manager

↓

Scheduler

↓

Kubelet

↓

Container Runtime

↓

Pod Running

Today we will learn what Kubernetes actually deploys.

---

# What is a Pod?

A Pod is the smallest deployable unit in Kubernetes.

Kubernetes never deploys Containers directly.

Instead, it deploys Pods, and Pods contain one or more containers.

Hierarchy

Kubernetes Cluster

↓

Worker Node

↓

Pod

↓

Container

---

# Why doesn't Kubernetes deploy Containers directly?

Suppose an application requires:

- Backend Application
- Logging Agent
- Monitoring Agent

If these run separately:

- Different Network
- Different Lifecycle
- Difficult Communication
- Separate Storage

Instead, Kubernetes groups related containers inside one Pod.

Example

+--------------------------------------+

| POD |

| |

| Backend Container |

| |

| Logging Container |

| |

| Monitoring Container |

+--------------------------------------+

All containers inside a Pod:

- Share Network
- Share Storage
- Share Lifecycle
- Communicate using localhost

---

# Single Container vs Multi-Container Pod

## Single Container Pod

Most commonly used.

Example

Pod

↓

Nginx Container

---

## Multi-Container Pod

Used when supporting containers are required.

Example

Pod

├── Backend Container

├── Fluent Bit (Logging)

└── Monitoring Agent

This design is commonly called the Sidecar Pattern.

---

# Interview Tip

Pod

=

Smallest Deployable Unit

Containers are scheduled through Pods.

---

# Why was ReplicaSet introduced?

Suppose we create one Pod.

Backend Pod

↓

Running

If it crashes:

↓

Application Down

If traffic increases:

One Pod is not enough.

Managing Pods manually becomes difficult.

Kubernetes introduced ReplicaSet.

---

# What is ReplicaSet?

ReplicaSet ensures that the desired number of Pods are always running.

Example

Desired Replicas = 3

Current Running = 2

↓

ReplicaSet creates 1 new Pod

---

# Internal Working

Desired State

↓

3 Pods

Current State

↓

2 Pods

↓

ReplicaSet detects mismatch

↓

Creates 1 New Pod

↓

Desired State Achieved

---

# Responsibilities of ReplicaSet

- Maintain Desired Replica Count
- Replace Failed Pods
- Automatically Create New Pods
- Self-Healing

---

# Interview Tip

ReplicaSet

=

Pod Manager

---

# Why Deployment?

ReplicaSet manages only the number of Pods.

It does NOT manage:

- Application Versions
- Rolling Updates
- Rollback
- Deployment History

Kubernetes introduced Deployment to solve these problems.

---

# What is Deployment?

Deployment is a higher-level Kubernetes object that manages ReplicaSets.

It provides:

- Rolling Updates
- Rollbacks
- Version History
- Declarative Updates
- Zero Downtime Deployment

---

# Kubernetes Hierarchy

Developer

↓

Deployment

↓

ReplicaSet

↓

Pods

↓

Containers

---

# Rolling Update

Current Version

Backend:v1

↓

Developer updates image

↓

Backend:v2

Deployment creates a new ReplicaSet.

ReplicaSet-v1

↓

ReplicaSet-v2

↓

Traffic shifts gradually

↓

Old ReplicaSet scaled down

No downtime occurs.

---

# Why Deployment creates a New ReplicaSet?

Instead of modifying the existing ReplicaSet, Deployment creates a new ReplicaSet because:

- Old Version remains available
- Rollback becomes possible
- Deployment History is preserved
- Safer Production Deployment

---

# Labels

Labels are key-value pairs attached to Kubernetes resources.

Example

labels:

app: backend

env: production

tier: api

Labels help identify and organize resources.

Think of Labels as Azure Resource Tags.

---

# Why not use Pod Names?

Pod Names change whenever Pods are recreated.

Labels remain consistent.

Therefore Kubernetes always uses Labels instead of Pod names.

---

# Selectors

Selectors search for Kubernetes objects using Labels.

Example

selector:

matchLabels:

app: backend

Kubernetes finds every Pod where:

app=backend

---

# Labels + Selectors Example

Pods

Pod-A

app=backend

env=prod

Pod-B

app=backend

env=dev

Pod-C

app=frontend

env=prod

Pod-D

app=backend

env=prod

Service Selector

selector:

app: backend

env: prod

Traffic goes to:

- Pod-A
- Pod-D

---

# Deployment YAML

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