# Docker Day 3 - Volumes, Networking & Logs

## Learning Objectives

- Understand Docker Volumes
- Learn Persistent Storage
- Understand Ephemeral Containers
- Learn Docker Networking
- Understand Docker DNS (Service Discovery)
- Learn Docker Inspect
- Learn Docker Logs

---

# 1. Docker Volumes

## What is a Docker Volume?

A Docker Volume is a Docker-managed persistent storage that exists independently of containers.

Even if a container is deleted, the volume and its data remain safe.

---

## Why do we need Docker Volumes?

Containers are temporary (Ephemeral).

If application data is stored inside the container, deleting the container will also delete the data.

Docker Volumes solve this problem by storing data outside the container.

---

## Real World Example

Suppose PostgreSQL stores customer data.

Without Volume:

PostgreSQL Container Deleted

↓

Customer Data Lost

With Volume:

PostgreSQL Container Deleted

↓

Volume Still Exists

↓

Customer Data Safe

---

## Create a Volume

```bash
docker volume create postgres-data
```

List Volumes

```bash
docker volume ls
```

---

## Mount a Volume

```bash
docker run -it \
--name ubuntu-volume-test \
-v postgres-data:/data \
ubuntu bash
```

---

# 2. Ephemeral Containers

Containers are temporary.

Containers can be created, stopped, deleted and recreated at any time.

Never store important application data inside a container.

Always use Docker Volumes.

---

# 3. Docker Networking

Docker Networking allows containers to communicate securely.

Containers in the same Docker Network can communicate with each other.

---

## Default Docker Networks

- bridge
- host
- none

bridge → Default network

host → Uses host machine's network (mainly on Linux)

none → No networking

---

## Custom Network

Create:

```bash
docker network create urbanx-network
```

Run a container in the network:

```bash
docker run -dit \
--name frontend \
--network urbanx-network \
ubuntu bash
```

---

# 4. Docker DNS (Service Discovery)

Docker automatically creates DNS entries for container names.

Instead of:

DB_HOST=172.18.0.2

Use:

DB_HOST=postgres

Docker automatically resolves:

postgres

↓

172.xx.xx.xx

---

## Why use container names instead of IP addresses?

Container IP addresses change whenever containers are recreated.

Container names remain the same.

Docker DNS automatically maps the latest IP.

---

# 5. Docker Inspect

Displays detailed information about a container.

Useful for checking:

- Image
- Network
- IP Address
- Mounts
- Environment Variables

Command:

```bash
docker inspect frontend
```

---

# 6. Docker Logs

Displays application logs.

```bash
docker logs nginx-demo
```

Live Logs

```bash
docker logs -f nginx-demo
```

---

# Key Learnings

✔ Containers are Ephemeral

✔ Volumes provide Persistent Storage

✔ Docker Networks enable container communication

✔ Docker DNS allows communication using container names

✔ docker inspect provides container configuration details

✔ docker logs helps troubleshoot applications