# ☸️ Kubernetes Day 02 - Interview Questions

---

## Q1. What is a Pod?

Answer

A Pod is the smallest deployable unit in Kubernetes. It contains one or more containers that share the same network, storage, and lifecycle.

---

## Q2. Why does Kubernetes use Pods instead of Containers?

Answer

Pods provide a logical wrapper around containers, allowing related containers to share networking, storage, and lifecycle.

---

## Q3. Can a Pod contain multiple containers?

Answer

Yes.

A Pod may contain one or more containers.

However, in production, most Pods contain only one application container unless sidecar containers are required.

---

## Q4. What is a ReplicaSet?

Answer

ReplicaSet ensures that the desired number of Pods are always running.

---

## Q5. What happens if one Pod crashes?

Answer

ReplicaSet detects that the desired state and current state differ and automatically creates another Pod.

---

## Q6. Why don't companies create Pods directly?

Answer

Pods are temporary.

In production, Deployments manage ReplicaSets, and ReplicaSets manage Pods.

---

## Q7. Difference between Pod and ReplicaSet?

Pod

Runs application.

ReplicaSet

Maintains the desired number of Pods.

---

## Q8. Difference between ReplicaSet and Deployment?

ReplicaSet

Maintains Pod count.

Deployment

Manages ReplicaSets and provides:

- Rolling Updates
- Rollbacks
- Version History

---

## Q9. Why does Deployment create a new ReplicaSet?

Answer

Deployment creates a new ReplicaSet whenever the Pod template changes (such as a new image version). This preserves deployment history, enables rolling updates, and allows rollback if required.

---

## Q10. What are Labels?

Answer

Labels are key-value pairs attached to Kubernetes resources to identify and organize them.

Example

```
app=backend
```

---

## Q11. What are Selectors?

Answer

Selectors identify Kubernetes resources using Labels.

---

## Q12. Why not use Pod Names?

Answer

Pod Names change whenever Pods are recreated.

Labels remain constant.

Therefore Kubernetes always uses Labels.

---

## Q13. What happens if selector.matchLabels doesn't match Pod Labels?

Answer

Deployment cannot identify its own Pods.

As a result, it cannot manage or scale them correctly.

---

## Q14. Explain Deployment Flow.

Answer

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

## Q15. Which Kubernetes object performs Rolling Updates?

Answer

Deployment.

---

## Q16. Can ReplicaSet perform Rollback?

Answer

No.

Rollback is managed by Deployment.

---

## Q17. Which object actually creates Pods?

Answer

ReplicaSet.

Deployment creates ReplicaSet, and ReplicaSet creates Pods.

---

## Q18. What is the hierarchy of Kubernetes objects?

Answer

Deployment

↓

ReplicaSet

↓

Pods

↓

Containers

---

## Q19. Why are Labels important?

Answer

Almost every Kubernetes object uses Labels to identify resources.

Services, Deployments, ReplicaSets, Network Policies, and Monitoring tools depend on Labels.

---

## Q20. Explain Desired State.

Answer

Desired State is the state defined inside the Kubernetes manifest.

Kubernetes continuously compares Desired State with Current State and takes corrective action whenever they differ. 
