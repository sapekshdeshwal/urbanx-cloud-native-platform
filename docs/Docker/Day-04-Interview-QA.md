# Docker Day 04 - Interview Questions & Answers

## Q1. What is Docker Compose?

### Answer

Docker Compose is a tool used to define and manage multi-container Docker applications using a YAML configuration file (docker-compose.yml). It allows us to start, stop, and manage multiple related containers with a single command.

Example:

Frontend

↓

Backend

↓

PostgreSQL

All can be started using:

```bash
docker compose up
```

---

## Q2. Why do we use Docker Compose?

### Answer

Without Docker Compose, we need to execute multiple docker run commands for each container.

Docker Compose automates:

- Container Creation
- Docker Network Creation
- Named Volume Creation
- Environment Variables
- Health Checks
- Restart Policies

Everything is managed using one YAML file.

---

## Q3. What is YAML?

### Answer

YAML (YAML Ain't Markup Language) is a human-readable configuration language used by Docker Compose.

It is indentation-sensitive.

Always use spaces instead of TAB.

---

## Q4. What is docker-compose.yml?

### Answer

docker-compose.yml is the configuration file used by Docker Compose.

It defines:

- Services
- Networks
- Volumes
- Environment Variables
- Restart Policies
- Health Checks

Docker reads this file to create the application stack.

---

## Q5. What is a Service in Docker Compose?

### Answer

A Service represents one container.

Example

```yaml
services:

  backend:
    image: ubuntu

  postgres:
    image: postgres
```

backend and postgres are Service Names.

Docker uses them for:

- Container Naming
- Docker DNS
- Network Communication

---

## Q6. Difference between image and build?

### Answer

image

Uses an existing Docker image.

Example

```yaml
image: postgres
```

build

Builds a new Docker image using Dockerfile.

Example

```yaml
build: ./backend
```

Interview Tip

If Docker Hub already has the image → image

If we created the application → build

---

## Q7. Why use build for Backend but image for PostgreSQL?

### Answer

Backend is our custom application.

Docker needs to build it using Dockerfile.

PostgreSQL already exists on Docker Hub.

Therefore Docker only downloads and runs it.

---

## Q8. What is the purpose of .env?

### Answer

The .env file stores configuration separately from the application.

Example

```env
POSTGRES_USER=urbanx
POSTGRES_PASSWORD=admin123
POSTGRES_DB=urbanx_db
```

This improves:

- Security
- Maintainability
- Reusability

---

## Q9. Why should we not hardcode passwords inside docker-compose.yml?

### Answer

Hardcoding passwords exposes sensitive information.

Best Practice

Store secrets in:

- .env
- Azure Key Vault
- AWS Secrets Manager
- HashiCorp Vault

---

## Q10. What is env_file?

### Answer

env_file tells Docker Compose to load environment variables from an external .env file.

Example

```yaml
env_file:
  - .env
```

Docker injects these variables into the container during startup.

---

## Q11. Does Docker understand POSTGRES_USER?

### Answer

No.

Docker simply passes the environment variables into the container.

The PostgreSQL application inside the container reads and uses these variables.

---

## Q12. What is a Named Volume?

### Answer

A Named Volume is Docker-managed persistent storage.

Example

```yaml
volumes:
  - postgres-data:/var/lib/postgresql/data
```

Database files remain safe even if the container is deleted.

---

## Q13. Why do databases use Docker Volumes?

### Answer

Containers are ephemeral.

If database files remain inside the container, deleting the container also deletes the data.

Volumes store data outside the container, ensuring persistence.

---

## Q14. What is Restart Policy?

### Answer

Restart Policy tells Docker what to do if a container stops.

Available options

- no
- always
- on-failure
- unless-stopped

---

## Q15. Difference between restart: always and restart: unless-stopped?

### Answer

restart: always

Container restarts after:

- Crash
- Docker Restart
- Server Reboot

restart: unless-stopped

Same behavior, but if the administrator manually stops the container, Docker respects that decision.

---

## Q16. What is a Health Check?

### Answer

Health Check verifies whether the application inside the container is actually healthy.

Running Container

≠

Healthy Application

---

## Q17. Why do we need Health Checks?

### Answer

A container can be running while the application inside is frozen or returning errors.

Health Checks verify that the application is responding correctly.

---

## Q18. Why do we use pg_isready?

### Answer

pg_isready checks whether PostgreSQL is accepting client connections.

It verifies application readiness rather than simply checking whether the container is running.

---

## Q19. Difference between Restart Policy and Health Check?

### Answer

Restart Policy

Controls what Docker should do after the container stops.

Health Check

Verifies whether the application inside the running container is healthy.

---

## Q20. What happens when we execute docker compose up?

### Answer

Docker performs the following steps

Read docker-compose.yml

↓

Read .env

↓

Create Network

↓

Create Named Volume

↓

Download Images

↓

Build Images (if required)

↓

Create Containers

↓

Attach Network

↓

Attach Volumes

↓

Inject Environment Variables

↓

Run Health Checks

↓

Application Ready

---

## Q21. Difference between docker compose up and docker compose up -d?

### Answer

docker compose up

Runs containers in foreground.

Displays logs.

docker compose up -d

Runs containers in detached (background) mode.

---

## Q22. What does docker compose down do?

### Answer

Stops and removes:

- Containers
- Default Network

Named Volumes remain unless explicitly removed.

---

## Q23. Does Docker Compose automatically create a network?

### Answer

Yes.

Docker Compose automatically creates a default bridge network.

All services join this network.

---

## Q24. How do containers communicate in Docker Compose?

### Answer

Containers communicate using Service Names.

Example

Backend connects to PostgreSQL using

```text
postgres
```

instead of IP Address.

Docker DNS automatically resolves the Service Name.

---

## Q25. Why should we avoid using Container IP Address?

### Answer

Container IP addresses change whenever the container is recreated.

Docker DNS automatically updates the Service Name.

Therefore Service Names should always be used.

---

## Q26. Why use command: sleep infinity?

### Answer

Ubuntu containers exit immediately if there is no foreground process.

sleep infinity keeps the container alive for development and testing.

---

## Q27. Why use docker compose instead of multiple docker run commands?

### Answer

Docker Compose provides:

- Automation
- Repeatability
- Version Control
- Easier Collaboration
- Simplified Multi-Container Management

---

## Q28. Explain Docker Compose in one minute.

### Answer

Docker Compose is a tool used to define and manage multi-container Docker applications using a docker-compose.yml file. It automatically creates containers, networks, volumes, and injects environment variables. It also supports restart policies and health checks, making it easier to manage complete applications using a single command.

---

## Q29. What are the best practices for Docker Compose?

### Answer

- Use .env for configuration.
- Never hardcode passwords.
- Use Named Volumes for databases.
- Use Health Checks.
- Use Restart Policies.
- Use Service Names instead of Container IPs.
- Use build for custom applications.
- Use image for official images.

---

## Q30. Explain your Day 04 project.

### Answer

I created a multi-container application using Docker Compose.

The project included:

- Backend Service
- PostgreSQL Database
- Docker Compose
- .env File
- Named Volumes
- Restart Policies
- Health Checks
- Docker Networking

Using Docker Compose, I managed the complete application with a single command while following production best practices like external configuration, persistent storage, automatic restart, and application health monitoring.

---

# Interview Summary

By completing Docker Day 04, I learned:

✔ Docker Compose

✔ YAML

✔ docker-compose.yml

✔ .env

✔ env_file

✔ image vs build

✔ Docker Networking

✔ Named Volumes

✔ Restart Policies

✔ Health Checks

✔ Docker Internal Working

✔ Production Best Practices

These concepts are widely used in real-world DevOps environments and form the foundation for Kubernetes deployments.
