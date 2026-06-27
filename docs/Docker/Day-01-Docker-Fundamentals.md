# Docker Day 1 - Docker Fundamentals

## 🎯 Objective

Learn the fundamentals of Docker, understand its architecture, images, containers, Docker Hub, and deploy the first web server using Nginx.

---

# Why Docker?

Before Docker, applications often worked on a developer's machine but failed on testing or production servers because of different operating systems, libraries, or software versions.

Docker solves this problem by packaging an application with all its dependencies into a portable container.

---

# What is Docker?

Docker is an open-source containerization platform that packages an application along with its dependencies into lightweight, portable containers.

**Key Benefits**

- Portability
- Consistency
- Fast Deployment
- Lightweight
- Easy Scaling

---

# Docker Architecture

```
Developer
    │
    ▼
Docker CLI
    │
    ▼
Docker Engine (Daemon)
    │
 ┌──┴──────────────┐
 ▼                 ▼
Docker Hub     Local Images
                     │
                     ▼
                Containers
```

---

# Components

## Docker CLI

Used by developers to interact with Docker.

Example:

```bash
docker run
docker pull
docker build
docker ps
```

---

## Docker Engine (Daemon)

The background service responsible for building, running and managing Docker containers.

---

## Docker Hub

A public image repository where Docker images are stored.

Example:

```bash
docker pull nginx
```

downloads the Nginx image from Docker Hub.

---

## Docker Image

A read-only template used to create containers.

Think of an Image as a **Blueprint**.

Example:

```
Nginx Image
```

---

## Docker Container

A running instance of a Docker Image.

Think of a Container as a **Running House built from the Blueprint**.

Example:

```bash
docker run nginx
```

---

# Image vs Container

| Docker Image | Docker Container |
|--------------|------------------|
| Blueprint | Running Application |
| Read Only | Read/Write |
| Cannot Execute | Executes Application |
| Reusable | Temporary |

---

# What is Nginx?

Nginx is a high-performance web server.

It receives requests from users and serves web pages.

Example:

```
Browser
    │
    ▼
 Nginx Web Server
    │
    ▼
index.html
```

---

# Container Lifecycle

```
Docker Image
      │
      ▼
docker run
      │
      ▼
Running Container
      │
      ├── docker stop
      ├── docker start
      ├── docker restart
      └── docker rm
```

---

# Docker Exec

Command:

```bash
docker exec -it my-nginx bash
```

Purpose:

Enter a running container for troubleshooting, checking files, logs, configuration, environment variables and processes.

---

# Real World Example

Suppose the UrbanX website is showing an error.

A DevOps Engineer will:

1. Check running containers
2. View container logs
3. Enter the running container
4. Inspect configuration
5. Verify environment variables
6. Troubleshoot the application

---

# Key Takeaways

- Docker packages applications with dependencies.
- Images are blueprints.
- Containers are running instances.
- Docker Hub stores Docker Images.
- Nginx is a web server.
- Docker Exec is used for troubleshooting running containers.