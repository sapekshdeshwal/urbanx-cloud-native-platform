# 🐳 Docker Day 2 – Dockerfile Fundamentals

## 🎯 Objective

Learn how Docker Images are built using Dockerfiles and understand the core Dockerfile instructions used in real-world DevOps projects.

---

# 📚 Topics Covered

- Dockerfile
- FROM
- COPY
- EXPOSE
- CMD
- RUN
- WORKDIR
- Docker Layers
- Docker Cache
- Image Immutability
- Build Context
- .dockerignore
- COPY vs ADD

---

# 🏗️ Docker Image Build Workflow

```text
Developer
    │
    ▼
Dockerfile
    │
docker build
    │
    ▼
Docker Image
    │
docker run
    │
    ▼
Docker Container
```

---

# What is a Dockerfile?

A Dockerfile is a text file containing a sequence of instructions that Docker uses to build an image.

Instead of manually configuring a server every time, we automate the entire process through a Dockerfile.

Think of it as a **blueprint** for creating Docker Images.

---

# Dockerfile Used During Practical

```dockerfile
FROM nginx

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

---

# FROM

The **FROM** instruction specifies the base image.

Example:

```dockerfile
FROM nginx
```

Everything in our image is built on top of the official Nginx image.

---

# COPY

The **COPY** instruction copies files from the local machine into the Docker Image.

Example:

```dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

In our project, we replaced the default Nginx web page with our own `index.html`.

---

# EXPOSE

The **EXPOSE** instruction documents the port on which the application listens.

```dockerfile
EXPOSE 80
```

> **Important:** EXPOSE does **not** publish the port.

Port publishing happens during:

```bash
docker run -p 8080:80 urbanx:v1
```

---

# CMD

CMD defines the default command executed when the container starts.

```dockerfile
CMD ["nginx","-g","daemon off;"]
```

This starts the Nginx web server.

---

## Why `daemon off;`?

Docker containers run only while the main process is running.

Normally Nginx runs in the background.

Using:

```dockerfile
daemon off;
```

keeps Nginx in the foreground, allowing the container to stay alive.

---

# RUN

RUN executes commands while building the Docker Image.

Example:

```dockerfile
RUN apt update

RUN apt install curl -y
```

RUN is executed only during:

```bash
docker build
```

and not when the container starts.

---

# RUN vs CMD

| RUN | CMD |
|------|------|
| Executes during image build | Executes when container starts |
| Used to install software | Used to start the application |
| Runs only once | Runs every time the container starts |

---

# WORKDIR

WORKDIR changes the current working directory inside the image.

```dockerfile
WORKDIR /app
```

All following instructions execute relative to `/app`.

Instead of writing:

```dockerfile
RUN cd /app
```

we use:

```dockerfile
WORKDIR /app
```

because it persists for all subsequent instructions.

---

# Docker Layers

Docker builds images layer by layer.

Example:

```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/
RUN apt update
```

Layers:

```text
Layer 1 → FROM nginx

Layer 2 → COPY index.html

Layer 3 → RUN apt update
```

---

# Docker Cache

Docker caches unchanged layers.

If the Dockerfile instruction hasn't changed, Docker reuses the cached layer instead of rebuilding it.

Example:

```text
CACHED [1/2] FROM nginx
```

This speeds up image builds.

---

# Image Immutability

Docker Images are immutable.

Once an image is created, it cannot be modified.

Changing the Dockerfile or application creates a **new image** instead of modifying the existing one.

Example:

```text
urbanx:v1

↓

Modify index.html

↓

urbanx:v2
```

---

# Build Context

Command:

```bash
docker build .
```

The dot (`.`) represents the Build Context.

Docker can access only files inside the Build Context.

Files outside the Build Context cannot be copied into the image.

---

# .dockerignore

`.dockerignore` excludes unnecessary files from the Build Context.

Example:

```text
.git
.vscode
node_modules
.env
*.log
```

Benefits:

- Faster image builds
- Smaller build context
- Better security
- Cleaner Docker Images

---

# COPY vs ADD

## COPY

Copies files from the local machine into the Docker Image.

```dockerfile
COPY app.py /app/
```

---

## ADD

ADD supports everything COPY does and can also:

- Extract local tar archives automatically.
- (Historically) Download remote URLs.

Example:

```dockerfile
ADD project.tar.gz /app/
```

---

## Best Practice

✅ Prefer **COPY**.

Use **ADD** only when its additional functionality is required.

---

# Key Learnings

- Dockerfile is the blueprint for creating Docker Images.
- Docker builds images layer by layer.
- Docker Cache speeds up builds.
- Docker Images are immutable.
- RUN executes during image build.
- CMD executes when the container starts.
- WORKDIR defines the current working directory.
- Build Context controls which files Docker can access.
- `.dockerignore` reduces build time and improves security.
- COPY is preferred over ADD in most production environments.

---

# Interview Tips

- Explain the difference between RUN and CMD.
- Explain Docker Layers and Docker Cache.
- Explain Image Immutability.
- Explain Build Context.
- Explain COPY vs ADD.
- Explain why `daemon off;` is required for Nginx.

---

# Summary

Dockerfile enables Infrastructure as Code for containers by automating image creation. Understanding Dockerfile instructions, Docker Layers, Docker Cache, Build Context, and image optimization is essential for building efficient, secure, and production-ready container images.