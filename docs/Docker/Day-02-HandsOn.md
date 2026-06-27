# 🐳 Docker Day 2 – Hands-on Practical

## 🎯 Objective

Build a custom Docker Image using a Dockerfile and understand how Docker creates images layer by layer.

---

# Project Structure

```
day-02/
│
├── Dockerfile
└── index.html
```

---

# Step 1 - Create index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>UrbanX</title>
</head>

<body style="text-align:center;margin-top:120px;font-family:Arial">

<h1>🚀 Welcome to UrbanX</h1>

<h2>Built using Docker</h2>

<p>Created by Sapeksh Deshwal</p>

</body>
</html>
```

---

# Step 2 - Create Dockerfile

```dockerfile
FROM nginx

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

---

# Step 3 - Build Docker Image

```bash
docker build -t urbanx:v1 .
```

### Explanation

- `docker build` → Build Docker Image
- `-t` → Tag Image
- `urbanx` → Image Name
- `v1` → Version
- `.` → Current directory is Build Context

---

# Verify Images

```bash
docker images
```

Expected Output

```
urbanx:v1

nginx:latest
```

---

# Run Container

```bash
docker run -d --name urbanx-container -p 8081:80 urbanx:v1
```

Explanation

- `-d` → Detached Mode
- `--name` → Container Name
- `-p` → Port Mapping

```
Host
8081

↓

Container
80
```

---

# Verify Running Containers

```bash
docker ps
```

---

# Open Browser

```
http://localhost:8081
```

Expected Output

```
🚀 Welcome to UrbanX

Built using Docker

Created by Sapeksh Deshwal
```

---

# Build Version 2

Modify

```
index.html
```

Build again

```bash
docker build -t urbanx:v2 .
```

Docker Output

```
CACHED [1/2] FROM nginx
```

Observation

Docker reused Layer 1 because nothing changed.

Only changed layers were rebuilt.

---

# Verify Images

```bash
docker images
```

Expected

```
urbanx:v1

urbanx:v2
```

---

# Container Name Conflict

Attempt

```bash
docker run --name urbanx-container urbanx:v2
```

Docker Error

```
Conflict

Container name already exists.
```

Reason

Container names must be unique.

Solution

```bash
docker run -d \
--name urbanx-v2-container \
-p 8082:80 \
urbanx:v2
```

---

# Commands Used

```bash
docker build -t urbanx:v1 .

docker build -t urbanx:v2 .

docker images

docker ps

docker run -d --name urbanx-container -p 8081:80 urbanx:v1

docker run -d --name urbanx-v2-container -p 8082:80 urbanx:v2
```

---

# Practical Learnings

- Built first custom Docker Image.
- Understood Dockerfile workflow.
- Understood Docker Layers.
- Understood Docker Cache.
- Understood Image Versioning.
- Understood Port Mapping.
- Understood Container Naming.
- Understood Image Immutability.

---

# Common Mistakes

❌ Forgetting the Build Context (`.`)

❌ Using the same container name twice

❌ Forgetting port mapping

❌ Expecting EXPOSE to publish ports

❌ Editing an existing Docker Image instead of creating a new one

---

# Summary

Successfully created two Docker Images (`urbanx:v1` and `urbanx:v2`), deployed them as containers, verified Docker Cache behavior, understood image immutability, and practiced the complete Docker image lifecycle from Dockerfile to running container.

