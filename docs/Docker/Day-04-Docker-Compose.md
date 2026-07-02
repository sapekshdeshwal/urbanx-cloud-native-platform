# Docker Day 04 - Docker Compose

## Objective

Learn how to manage multi-container applications using Docker Compose.

By the end of this session, you will understand:

- What is Docker Compose?
- Why Docker Compose is required?
- YAML Basics
- docker-compose.yml
- .env file
- image vs build
- Docker Compose Networking
- Named Volumes
- Restart Policies
- Health Checks
- Production Best Practices

---

# What is Docker Compose?

Docker Compose is a tool used to define, configure and manage multiple Docker containers using a single YAML file.

Instead of running multiple docker run commands, Docker Compose allows us to define the entire application inside one file.

Example

UrbanX Application

Frontend

Backend

PostgreSQL

All these containers can be started together using:

```bash
docker compose up
```

---

# Why Docker Compose?

Suppose we have an application consisting of:

- Frontend
- Backend
- PostgreSQL Database

Without Docker Compose

```bash
docker run nginx

docker run postgres

docker run ubuntu
```

Need to create every container manually.

Need to connect them manually.

Need to configure networking manually.

Need to configure volumes manually.

Very difficult for large applications.

---

With Docker Compose

```bash
docker compose up
```

Docker automatically

- Creates Network
- Creates Containers
- Creates Volumes
- Injects Environment Variables
- Starts Application

Everything happens using a single command.

---

# What is YAML?

Docker Compose uses YAML (YAML Ain't Markup Language).

YAML is a human-readable configuration language.

Example

```yaml
services:

  backend:
    image: ubuntu
```

YAML depends on indentation.

Never use TAB.

Always use spaces.

Wrong

backend:

image: ubuntu

Correct

backend:
  image: ubuntu

Interview Tip

YAML is indentation-sensitive.

---

# docker-compose.yml

This file contains the complete application configuration.

Example

```yaml
services:

  backend:
    image: ubuntu

  postgres:
    image: postgres
```

Docker reads this file and creates the required resources.

---

# Complete Docker Compose File

```yaml
services:

  backend:
    image: ubuntu
    command: sleep infinity
    restart: unless-stopped

  postgres:
    image: postgres

    env_file:
      - .env

    restart: always

    volumes:
      - postgres-data:/var/lib/postgresql/data

    healthcheck:
      test: ["CMD-SHELL","pg_isready -U $$POSTGRES_USER"]
      interval: 30s
      timeout: 10s
      retries: 5

volumes:
  postgres-data:
```

---

# Code Explanation (Line by Line)

## services:

Purpose

Root section of Docker Compose.

Every application service is defined under this section.

Docker Internal Working

docker-compose.yml

↓

Read services

↓

backend

↓

postgres

↓

Need to create 2 containers

Interview Question

Q. What is services?

Answer

Root section where all application containers are defined.

---

## backend:

Purpose

Service Name.

Not Image Name.

Docker uses it for

- Container Name
- Docker DNS
- Network Alias

Example

Backend container can be accessed using

backend

instead of IP Address.

---

## image:

Example

```yaml
image: postgres
```

Purpose

Use an existing image.

Docker Internal Working

Check Local Images

↓

Found?

↓

YES

↓

Use Image

↓

NO

↓

Pull from Docker Hub

↓

Create Container

Examples

- nginx
- postgres
- redis
- ubuntu

Interview Tip

If Docker Hub already has the image

Use

image

---

## build:

Example

```yaml
build: ./backend
```

Purpose

Build Docker Image using Dockerfile.

Used for our own applications.

Examples

Backend

Frontend

Python Application

Java Application

Interview Tip

If you created the application

Use

build

Memory Trick

Docker Hub already has it

↓

image

You created it

↓

build

---

## command

Example

```yaml
command: sleep infinity
```

Purpose

Keep Ubuntu container running.

Normally

Ubuntu

↓

Starts

↓

Bash exits

↓

Container stops

Using

sleep infinity

↓

Container keeps running forever.

Used for testing and development.

---

## env_file

Example

```yaml
env_file:
  - .env
```

Purpose

Read environment variables from external file.

Example

.env

```text
POSTGRES_USER=urbanx
POSTGRES_PASSWORD=admin123
POSTGRES_DB=urbanx_db
```

Docker Internal Working

Read .env

↓

Inject Variables

↓

Start PostgreSQL

Important

Docker does not understand POSTGRES_USER.

PostgreSQL understands it.

Docker only passes the variables.

Production Best Practice

Never hardcode passwords inside docker-compose.yml.

Store them in

.env

or

Azure Key Vault

AWS Secrets Manager

---

## restart

Purpose

Automatically restart containers.

Options

restart: no

restart: always

restart: on-failure

restart: unless-stopped

Production Recommendation

Backend

restart: unless-stopped

Database

restart: always

Difference

always

Restart after

- Crash
- Docker Restart
- Server Reboot

unless-stopped

Same as always

But respects manual stop.

---

## volumes

Example

```yaml
volumes:
  - postgres-data:/var/lib/postgresql/data
```

Purpose

Persist Database Data.

Without Volume

Database

↓

Container Deleted

↓

Database Deleted

With Volume

Database

↓

Docker Volume

↓

Container Deleted

↓

Database Safe

Interview Question

Why Docker Volume?

Answer

Containers are ephemeral.

Volumes provide persistent storage.

---

## healthcheck

Purpose

Verify application health.

Running Container

≠

Healthy Application

Docker executes

pg_isready

If PostgreSQL accepts connection

Healthy

Else

Unhealthy

---

## interval

Docker performs Health Check every

30 seconds.

---

## timeout

Docker waits

10 seconds.

No response

↓

Health Check Failed.

---

## retries

Docker retries

5 times.

After 5 failures

↓

Marks Container

UNHEALTHY

---

# Docker Compose Networking

Docker Compose automatically creates a network.

Example

Frontend

↓

Backend

↓

PostgreSQL

Every container joins the same network.

Docker DNS automatically resolves

backend

postgres

frontend

Therefore

Backend connects to PostgreSQL using

postgres

instead of IP Address.

Interview Question

Why should we avoid using Container IP?

Answer

Container IP changes after recreation.

Docker DNS automatically updates Service Name.

---

# Docker Compose Internal Working

When we execute

```bash
docker compose up
```

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

Start Containers

↓

Run Health Checks

↓

Application Ready

---

# Production Best Practices

✔ Use .env for configuration.

✔ Never hardcode passwords.

✔ Use Named Volumes for databases.

✔ Use Health Checks.

✔ Use Restart Policies.

✔ Use build for custom applications.

✔ Use image for official images.

✔ Use Service Names instead of Container IPs.

---

# Common Interview Questions

Q1 Why Docker Compose?

To manage multi-container applications using a single YAML file.

---

Q2 Difference between image and build?

image

Use existing image.

build

Create image using Dockerfile.

---

Q3 Why .env?

Separate configuration from application.

---

Q4 Why Docker Volume?

Persistent storage.

---

Q5 Why Health Check?

Running container does not guarantee healthy application.

---

Q6 Why Restart Policy?

Automatically recover containers after failure.

---

Q7 Why use Service Name instead of IP?

Docker DNS automatically updates Service Names.

Container IP changes.

---

# Summary

Today we learned

✔ Docker Compose

✔ YAML

✔ docker-compose.yml

✔ .env

✔ image vs build

✔ Docker Compose Networking

✔ Named Volumes

✔ Restart Policies

✔ Health Checks

✔ Docker Internal Working

✔ Production Best Practices

Docker Compose is one of the most important DevOps tools because it allows developers to define and run complete multi-container applications using a single configuration file.
