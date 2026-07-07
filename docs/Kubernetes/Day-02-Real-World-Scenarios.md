# ☸️ Kubernetes Day 02 - Real World Scenarios

---

# Scenario 1

Problem

UrbanX suddenly receives 20,000 users.

Question

Can one Pod handle all traffic?

Answer

No.

Increase replicas using Deployment.

Deployment

↓

ReplicaSet

↓

More Pods

↓

Load distributed.

---

# Scenario 2

Problem

One Backend Pod crashes.

Question

Who creates another Pod?

Answer

ReplicaSet.

ReplicaSet compares Desired State with Current State and creates one new Pod.

---

# Scenario 3

Problem

Entire Worker Node crashes.

Question

Can Kubelet restart Pods?

Answer

No.

The Kubelet on the failed node is unavailable.

Controller Manager detects the mismatch, Scheduler selects a healthy node, and the Kubelet on that node creates replacement Pods.

---

# Scenario 4

Problem

Developer releases Backend:v2.

Question

How does Kubernetes deploy the new version?

Answer

Deployment creates a new ReplicaSet.

↓

New Pods are created.

↓

Traffic shifts gradually.

↓

Old Pods removed.

This process is called Rolling Update.

---

# Scenario 5

Problem

Users report issues after deploying v2.

Question

How do you recover quickly?

Answer

Deployment supports Rollback.

Kubernetes scales the previous ReplicaSet back up and restores the earlier version.

---

# Scenario 6

Problem

Service cannot reach Backend Pods.

Question

What is the first thing to check?

Answer

Verify Labels and Selectors.

Commands

```bash
kubectl get pods --show-labels
kubectl describe service
```

---

# Scenario 7

Problem

A Pod is deleted accidentally.

Question

Will the application stop?

Answer

No.

ReplicaSet automatically creates another Pod.

---

# Scenario 8

Problem

Developer changes image from nginx:v1 to nginx:v2.

Question

Why doesn't Kubernetes modify the existing ReplicaSet?

Answer

ReplicaSets represent immutable Pod templates.

Deployment creates a new ReplicaSet to preserve version history and support safe rolling updates and rollbacks.

---

# Scenario 9

Problem

Kubernetes returns:

```
Unable to connect to localhost:8080
```

Question

Root Cause?

Answer

- Kubernetes Cluster not running
- API Server unavailable
- Current Context not configured

Resolution

- Enable Kubernetes
- Wait until the cluster is Ready
- Verify using:

```bash
kubectl cluster-info
kubectl get nodes
```

---

# Scenario 10

Problem

An interviewer asks:

"Why don't companies create Pods directly?"

Answer

Pods are temporary.

Production environments use Deployments because they provide version control, rolling updates, rollback capabilities, and high availability through ReplicaSets. 
