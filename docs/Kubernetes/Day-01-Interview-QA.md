# ☸️ Kubernetes Day 01 - Interview Questions & Answers

---

# Q1. What is Kubernetes?

## Answer

Kubernetes (K8s) is an open-source container orchestration platform used to deploy, manage, scale, and maintain containerized applications across multiple servers automatically.

It provides features like:

- Self-Healing
- Auto Scaling
- Load Balancing
- High Availability
- Rolling Updates
- Auto Rollbacks

---

# Q2. Why was Kubernetes created?

## Answer

Docker is excellent for running containers on a single machine.

However, production environments require:

- Multiple Servers
- Automatic Scaling
- High Availability
- Self-Healing
- Load Balancing

Kubernetes solves these problems by managing containers across an entire cluster.

---

# Q3. Why is Docker Compose not suitable for Production?

## Answer

Docker Compose is mainly designed for a single machine.

It cannot provide:

- Multi-node cluster management
- Automatic scheduling
- Self-healing across servers
- High availability
- Automatic scaling

Kubernetes provides all these features.

---

# Q4. What is a Kubernetes Cluster?

## Answer

A Kubernetes Cluster is a group of machines working together to run containerized applications.

It consists of:

- Control Plane
- One or More Worker Nodes

---

# Q5. Difference between Control Plane and Worker Node?

## Answer

| Control Plane | Worker Node |
|---------------|-------------|
| Makes decisions | Runs applications |
| Stores cluster state | Runs Pods |
| Schedules Pods | Executes workloads |
| Monitors cluster | Reports Pod status |

---

# Q6. What is the API Server?

## Answer

The API Server is the central entry point of Kubernetes.

It:

- Authenticates users
- Authorizes requests
- Validates YAML
- Stores desired state in etcd
- Coordinates other Kubernetes components

Interview Tip:

API Server = Front Door of Kubernetes

---

# Q7. What happens when we execute kubectl apply -f deployment.yaml?

## Answer

1. Request reaches API Server.
2. API Server authenticates the user.
3. API Server authorizes the request.
4. API Server validates the YAML.
5. Desired state is stored in etcd.
6. Controller Manager checks desired vs current state.
7. Scheduler selects the best Worker Node.
8. Kubelet instructs the Container Runtime.
9. Container Runtime creates the container.
10. Kubelet reports Pod status back to the API Server.

---

# Q8. What is etcd?

## Answer

etcd is a distributed key-value database that stores the complete Kubernetes cluster state.

It stores:

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets
- Namespaces

Interview Tip:

etcd = Cluster Memory

---

# Q9. Why is etcd important?

## Answer

The desired state of the cluster is stored in etcd.

Whenever Kubernetes needs to compare the desired state with the current state, it reads the information from etcd.

Without etcd, Kubernetes cannot remember the cluster configuration.

---

# Q10. What happens if etcd is lost?

## Answer

The cluster loses its stored state.

Kubernetes will not know:

- Desired Pods
- Deployments
- Services
- Secrets
- ConfigMaps

Therefore, regular etcd backups are critical in production.

---

# Q11. What is the Controller Manager?

## Answer

The Controller Manager continuously compares the desired state stored in etcd with the current state of the cluster.

If there is any difference, it takes corrective action.

Interview Tip:

Controller Manager = Supervisor

---

# Q12. What is Self-Healing?

## Answer

Self-Healing is Kubernetes' ability to automatically detect failed Pods or unhealthy nodes and recreate Pods on healthy Worker Nodes to maintain the desired state.

---

# Q13. What is the Scheduler?

## Answer

The Scheduler selects the most appropriate Worker Node for newly created Pods.

It considers:

- CPU
- Memory
- Node Health
- Resource Availability

Interview Tip:

Scheduler chooses.

It does not create Pods.

---

# Q14. Does the Scheduler create Pods?

## Answer

No.

The Scheduler only selects the Worker Node.

The Kubelet on that Worker Node creates the Pod.

---

# Q15. What is Kubelet?

## Answer

Kubelet is an agent running on every Worker Node.

It:

- Creates Pods
- Monitors Pods
- Reports Pod status
- Communicates with the Container Runtime

Interview Tip:

Kubelet = Worker

---

# Q16. Where does Kubelet run?

## Answer

Kubelet runs on every Worker Node.

One Worker Node = One Kubelet

---

# Q17. What is Container Runtime?

## Answer

Container Runtime is responsible for:

- Pulling images
- Creating containers
- Starting containers
- Stopping containers
- Managing the container lifecycle

Examples:

- containerd
- CRI-O

---

# Q18. Does Kubelet create containers directly?

## Answer

No.

Kubelet instructs the Container Runtime, which creates and starts the containers.

---

# Q19. What is kube-proxy?

## Answer

kube-proxy is a networking component that runs on every Worker Node.

It forwards traffic from Kubernetes Services to the appropriate Pods.

Interview Tip:

kube-proxy = Traffic Police

---

# Q20. Why do we need kube-proxy?

## Answer

Pods have dynamic IP addresses.

kube-proxy ensures that traffic sent to a Kubernetes Service is forwarded to the correct running Pods.

---

# Q21. Which component stores the cluster state?

## Answer

etcd

---

# Q22. Which component receives all requests?

## Answer

API Server

---

# Q23. Which component compares desired state with current state?

## Answer

Controller Manager

---

# Q24. Which component selects the Worker Node?

## Answer

Scheduler

---

# Q25. Which component creates Pods?

## Answer

Kubelet (with the help of the Container Runtime)

---

# Q26. Which component pulls container images?

## Answer

Container Runtime

---

# Q27. Which component routes network traffic?

## Answer

kube-proxy

---

# Q28. Explain Kubernetes Architecture in one minute.

## Answer

A Kubernetes Cluster consists of a Control Plane and one or more Worker Nodes.

The Control Plane receives requests, stores the cluster state, monitors the desired state, and schedules workloads.

Worker Nodes execute the workloads using Kubelet, Container Runtime, and kube-proxy.

---

# Q29. Explain the Kubernetes request flow.

## Answer

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

↓

Kubelet reports status

↓

API Server Updated

---

# Q30. Explain Kubernetes using a company analogy.

## Answer

- API Server → Receptionist
- etcd → Company Records
- Controller Manager → Supervisor
- Scheduler → HR Manager
- Kubelet → Employee
- Container Runtime → Machine Operator
- kube-proxy → Traffic Manager

Each component has a specific responsibility, and together they ensure applications run reliably across the cluster.

---

# Day 01 Interview Summary

By completing Day 01, you can confidently explain:

✅ Why Kubernetes

✅ Docker vs Kubernetes

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

These concepts form the foundation of Kubernetes and are among the most frequently asked topics in DevOps interviews.
