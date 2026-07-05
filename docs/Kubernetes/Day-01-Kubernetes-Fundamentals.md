# ☸️ Kubernetes Day 01 - Kubernetes Fundamentals

---

# Learning Objectives

By the end of Day 01, you will understand:

- Why Kubernetes was created
- Limitations of Docker Compose
- Kubernetes Architecture
- Control Plane vs Worker Node
- API Server
- etcd
- Controller Manager
- Scheduler
- Kubelet
- Container Runtime
- kube-proxy
- Complete Kubernetes Request Flow

---

# What is Kubernetes?

Kubernetes (K8s) is an open-source container orchestration platform used to deploy, manage, scale, and maintain containerized applications across multiple servers automatically.

It helps organizations run applications reliably in production by providing features like:

- Self-Healing
- Auto Scaling
- Load Balancing
- High Availability
- Rolling Updates
- Auto Rollbacks

---

# Why was Kubernetes Created?

Docker is excellent for creating and running containers.

However, Docker alone is not enough for managing applications running across hundreds of servers.

Example:

UrbanX initially has

- 1 Frontend Container
- 1 Backend Container
- 1 PostgreSQL Container

Docker Compose works perfectly.

As the application grows:

- 20 Frontend Pods
- 50 Backend Pods
- Redis
- Monitoring
- Multiple Databases
- Hundreds of Servers

Managing everything manually becomes almost impossible.

Kubernetes solves this problem.

---

# Docker Compose vs Kubernetes

## Docker Compose

- Works on a single machine
- Suitable for Development
- Manual Scaling
- Limited High Availability
- No Cluster Management

## Kubernetes

- Works on Multiple Servers
- Designed for Production
- Automatic Scaling
- Self-Healing
- Cluster Management
- High Availability

---

# What is a Kubernetes Cluster?

A Kubernetes Cluster is a collection of machines working together to run containerized applications.

A cluster consists of:

- Control Plane
- One or More Worker Nodes

Architecture

                    Kubernetes Cluster

        ┌────────────────────────────┐
        │      Control Plane         │
        └────────────────────────────┘
                     │
      ┌──────────────┼──────────────┐
      ▼              ▼              ▼
 Worker Node     Worker Node    Worker Node

---

# Control Plane

The Control Plane is the brain of Kubernetes.

It makes decisions for the entire cluster.

Responsibilities

- Receives Requests
- Stores Cluster State
- Schedules Pods
- Maintains Desired State
- Monitors Cluster Health

Components

- API Server
- etcd
- Controller Manager
- Scheduler

---

# Worker Node

Worker Nodes execute the workloads.

Every Worker Node contains:

- Kubelet
- Container Runtime
- kube-proxy

Responsibilities

- Run Pods
- Create Containers
- Monitor Pods
- Handle Networking

---

# API Server

## What is it?

The API Server is the central entry point of Kubernetes.

Every request first reaches the API Server.

Think of it as:

Front Door of Kubernetes

---

## Responsibilities

- Authenticate User
- Authorize Request
- Validate YAML
- Store Desired State in etcd
- Communicate with Control Plane Components

---

## Internal Working

Developer

↓

kubectl apply

↓

API Server

↓

Authenticate

↓

Authorize

↓

Validate

↓

Store in etcd

---

## Interview Tip

Remember

API Server

=

Front Door

---

# etcd

## What is it?

etcd is a distributed key-value database.

It stores the complete state of the Kubernetes Cluster.

Think of it as:

Memory of Kubernetes

---

## Stores

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets
- Namespaces
- Cluster State

---

## Why is it Important?

Whenever Kubernetes needs to know the desired state of the cluster, it reads the information from etcd.

Without etcd, Kubernetes cannot remember the cluster state.

---

## Interview Tip

etcd

=

Cluster Memory

---

# Controller Manager

## What is it?

The Controller Manager continuously compares:

Desired State

vs

Current State

If they are different, it takes corrective action.

---

## Responsibilities

- Monitor Cluster
- Detect Failed Pods
- Maintain Desired State
- Trigger Corrective Actions

---

## Example

Desired Pods = 5

Current Pods = 3

Controller Manager detects mismatch.

↓

Requests creation of 2 more Pods.

---

## Interview Tip

Controller Manager

=

Supervisor

---

# Scheduler

## What is it?

The Scheduler selects the most appropriate Worker Node for newly created Pods.

---

## Checks

- CPU Availability
- Memory Availability
- Node Health
- Resource Requests

---

## Example

Node-1

CPU = 95%

Node-2

CPU = 30%

Scheduler selects

Node-2

---

## Interview Tip

Scheduler

=

Decision Maker

---

# Kubelet

## What is it?

Kubelet is an agent running on every Worker Node.

It communicates with the API Server and ensures Pods are running correctly.

---

## Responsibilities

- Create Pods
- Monitor Pods
- Report Pod Status
- Communicate with Container Runtime

---

## Interview Tip

Scheduler chooses

Kubelet creates

---

# Container Runtime

## What is it?

Container Runtime is responsible for pulling images, creating containers, starting containers, and managing their lifecycle.

Examples

- containerd
- CRI-O

---

## Responsibilities

- Pull Images
- Create Containers
- Start Containers
- Stop Containers

---

## Interview Tip

Container Runtime

=

Engine

---

# kube-proxy

## What is it?

kube-proxy is the networking component running on every Worker Node.

It forwards Service traffic to the correct Pods.

---

## Responsibilities

- Maintain Network Rules
- Route Traffic
- Forward Requests
- Enable Pod Communication

---

## Interview Tip

kube-proxy

=

Traffic Police

---

# Complete Kubernetes Request Flow

Developer

↓

kubectl apply -f deployment.yaml

↓

API Server

↓

Authenticate

↓

Authorize

↓

Validate

↓

Store Desired State

↓

etcd

↓

Controller Manager

↓

Compare Desired vs Current State

↓

Scheduler

↓

Choose Worker Node

↓

Kubelet

↓

Container Runtime

↓

Pod Running

↓

Kubelet Reports Status

↓

API Server Updated

↓

kube-proxy Routes Traffic

---

# Real Company Example

Imagine Vodafone wants to deploy a new Backend application.

The DevOps Engineer executes:

kubectl apply -f backend.yaml

Kubernetes automatically:

- Validates the request
- Stores cluster state
- Chooses the best Worker Node
- Creates Pods
- Starts Containers
- Monitors Pod Health
- Routes user traffic

No manual server login is required.

---

# Day 01 Summary

Today we learned:

✅ Why Kubernetes

✅ Kubernetes Cluster

✅ Control Plane

✅ Worker Node

✅ API Server

✅ etcd

✅ Controller Manager

✅ Scheduler

✅ Kubelet

✅ Container Runtime

✅ kube-proxy

✅ Complete Request Flow

These concepts form the foundation of Kubernetes and are frequently asked in DevOps interviews.

