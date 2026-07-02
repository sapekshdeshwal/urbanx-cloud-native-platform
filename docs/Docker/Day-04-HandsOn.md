# Docker Day 04 - Hands-On

## Objective

In this hands-on session, we learned how to manage a multi-container application using Docker Compose.

We created:

- Docker Compose File
- Environment Variables
- Named Volumes
- Docker Network
- Restart Policies
- Health Checks

---

# Lab Setup

## Project Structure

```text
UrbanX-Cloud-Native-Platform/

docker/
└── Day-04/
    ├── docker-compose.yml
    └── .env
```

---

# Step 1 - Create Project Directory

```bash
mkdir Day-04
cd Day-04
```

Expected Result

Project folder created.

---

# Step 2 - Create docker-compose.yml

```bash
touch docker-compose.yml
```

Expected Result

Docker Compose configuration file created.

---

# Step 3 - Create .env File

```bash
touch .env
```

Add the following content

```env
POSTGRES_USER=urbanx
POSTGRES_PASSWORD=admin123
POSTGRES_DB=urbanx_db
```

Purpose

Store application configuration separately from docker-compose.yml.

---

# Step 4 - Write docker-compose.yml

Created the following services

- Backend
- PostgreSQL

Configured

- image
- command
- restart
- env_file
- volumes
- healthcheck

Learning

Docker Compose can manage multiple containers using a single YAML file.

---

# Step 5 - Start Application

```bash
docker compose up
```

Purpose

Start all services in foreground mode.

Expected Result

Docker

- Reads docker-compose.yml
- Creates Network
- Creates Volume
- Downloads Images
- Creates Containers
- Displays Logs

---

# Step 6 - Run in Detached Mode

```bash
docker compose up -d
```

Purpose

Run containers in background.

Verify

```bash
docker ps
```

Expected Result

Backend

PostgreSQL

Running

---

# Step 7 - Verify Containers

```bash
docker ps
```

Purpose

List running containers.

Expected Result

```text
backend

postgres
```

Both containers should be in Up state.

---

# Step 8 - Verify Docker Network

```bash
docker network ls
```

Expected Result

```text
day-04_default
```

Learning

Docker Compose automatically creates a default network.

---

# Step 9 - Verify Named Volume

```bash
docker volume ls
```

Expected Result

```text
postgres-data
```

Learning

Docker Compose automatically creates named volumes.

---

# Step 10 - Verify Logs

```bash
docker compose logs
```

Purpose

Display logs of all services.

---

Follow Live Logs

```bash
docker compose logs -f
```

Purpose

Monitor logs in real time.

Observation

When PostgreSQL starts successfully

Example

```text
database system is ready to accept connections
```

Learning

Logs help troubleshoot application issues.

---

# Step 11 - Inspect Container

```bash
docker inspect <container-name>
```

Example

```bash
docker inspect day-04-postgres-1
```

Verify

- Network
- IP Address
- Environment Variables
- Health Status
- Mounted Volumes

Learning

docker inspect provides detailed container information.

---

# Step 12 - Verify Health Check

```bash
docker inspect day-04-postgres-1
```

Search

```text
Health
```

Expected Result

```text
Healthy
```

Learning

Docker Health Check verifies whether PostgreSQL is accepting connections.

---

# Step 13 - Verify Docker Network Communication

Open Backend Container

```bash
docker exec -it day-04-backend-1 bash
```

Verify DNS

```bash
ping postgres
```

Expected Result

Backend resolves

```text
postgres
```

Learning

Docker DNS automatically resolves service names.

No need to use container IP.

---

# Step 14 - Stop Application

```bash
docker compose down
```

Purpose

Stop and remove

- Containers
- Default Network

Learning

Named Volumes remain unless explicitly removed.

---

# Step 15 - Restart Application

```bash
docker compose up -d
```

Learning

Containers are recreated.

Named Volume still contains PostgreSQL data.

---

# Step 16 - Verify Restart Policy

Restart Docker Desktop or stop/start the container.

Observe

Backend

```yaml
restart: unless-stopped
```

PostgreSQL

```yaml
restart: always
```

Learning

Restart policies improve application availability.

---

# Step 17 - Verify Health Status

```bash
docker ps
```

Container may show

```text
Up (healthy)
```

Learning

Container is running and application passed health checks.

---

# Common Commands Used

## Start Application

```bash
docker compose up
```

---

## Start in Background

```bash
docker compose up -d
```

---

## Stop Application

```bash
docker compose down
```

---

## View Running Containers

```bash
docker ps
```

---

## View All Containers

```bash
docker ps -a
```

---

## View Logs

```bash
docker compose logs
```

---

## Follow Logs

```bash
docker compose logs -f
```

---

## Restart Containers

```bash
docker compose restart
```

---

## Inspect Container

```bash
docker inspect <container-name>
```

---

## View Networks

```bash
docker network ls
```

---

## View Volumes

```bash
docker volume ls
```

---

## Enter Container

```bash
docker exec -it <container-name> bash
```

---

# Practical Learning Summary

During this hands-on session, we learned:

✔ Create a Docker Compose file

✔ Create a .env file

✔ Start multiple containers using Docker Compose

✔ Run containers in detached mode

✔ View running containers

✔ Inspect Docker networks

✔ Inspect Docker volumes

✔ View logs

✔ Inspect container details

✔ Verify Docker Health Checks

✔ Verify Docker DNS communication

✔ Stop and restart applications

✔ Understand restart policies

✔ Verify persistent storage using Named Volumes

---

# Key Takeaways

- Docker Compose simplifies multi-container management.
- Docker automatically creates a default network.
- Service names act as DNS names.
- Named Volumes preserve database data.
- .env files separate configuration from code.
- Restart policies improve availability.
- Health checks verify application health.
- Docker Compose is widely used for local development and testing before deploying applications to Kubernetes.
