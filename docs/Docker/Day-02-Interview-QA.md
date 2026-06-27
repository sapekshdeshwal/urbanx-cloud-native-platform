# 🎤 Docker Day 2 - Interview Questions & Answers

## 🎯 Objective

Revise the most commonly asked Docker interview questions related to Dockerfile, Docker Images, Layers, Cache, Build Context, and Dockerfile instructions.

---

# 1. What is a Dockerfile?

**Answer:**

A Dockerfile is a text file containing a set of instructions used by Docker to build an image automatically.

---

# 2. What is the purpose of FROM?

**Answer:**

FROM specifies the base image on which the new Docker image will be built.

Example:

```dockerfile
FROM nginx
```

---

# 3. What is COPY?

**Answer:**

COPY copies files and directories from the local machine into the Docker Image.

Example:

```dockerfile
COPY app.py /app/
```

---

# 4. What is EXPOSE?

**Answer:**

EXPOSE documents the port on which the application inside the container listens.

It **does not publish the port**.

---

# 5. How do you publish a port?

**Answer:**

Using the `-p` option.

Example:

```bash
docker run -p 8080:80 nginx
```

---

# 6. What is CMD?

**Answer:**

CMD specifies the default command that runs when the container starts.

---

# 7. Why do we use `daemon off;` with Nginx?

**Answer:**

Docker containers stay alive only while the main process is running.

`daemon off;` keeps Nginx running in the foreground.

---

# 8. What is RUN?

**Answer:**

RUN executes commands during image build.

Example:

```dockerfile
RUN apt update
```

---

# 9. Difference between RUN and CMD?

| RUN | CMD |
|------|------|
| Executes during build | Executes during container startup |
| Installs software | Starts the application |

---

# 10. What is WORKDIR?

**Answer:**

WORKDIR sets the current working directory for all subsequent Dockerfile instructions.

---

# 11. Why is WORKDIR preferred over `RUN cd`?

**Answer:**

`RUN cd` affects only that single RUN instruction.

WORKDIR changes the working directory for all following instructions.

---

# 12. What are Docker Layers?

**Answer:**

Docker Images are built layer by layer.

Each major Dockerfile instruction creates a new filesystem layer.

---

# 13. What is Docker Cache?

**Answer:**

Docker reuses unchanged layers to avoid rebuilding them, making image builds much faster.

---

# 14. What does this mean?

```
CACHED [1/2]
```

**Answer:**

Docker reused the cached layer because nothing changed in that instruction.

---

# 15. What is Image Immutability?

**Answer:**

Docker Images are immutable.

Once created, they cannot be modified.

A new image is created whenever changes are made.

---

# 16. Difference between Image and Container?

| Image | Container |
|--------|-----------|
| Template | Running instance |
| Read-only | Running process |
| Immutable | Temporary |

---

# 17. Difference between `docker pull`, `docker build`, and `docker run`?

| Command | Purpose |
|----------|---------|
| docker pull | Download image |
| docker build | Create image |
| docker run | Start container |

---

# 18. What is Build Context?

**Answer:**

Build Context is the set of files Docker can access during image build.

It is determined by the path passed to:

```bash
docker build .
```

---

# 19. Can Docker access files outside the Build Context?

**Answer:**

No.

Docker cannot access files outside the Build Context.

---

# 20. Why do we use `.dockerignore`?

**Answer:**

To exclude unnecessary files from the Build Context.

Benefits:

- Faster builds
- Smaller images
- Better security

---

# 21. Difference between COPY and ADD?

| COPY | ADD |
|------|------|
| Copies files | Copies + Extracts archives |
| Preferred | Use only when needed |

---

# 22. Which instruction is recommended?

**Answer:**

COPY.

It is simpler, predictable, and follows Docker best practices.

---

# 23. Why should `requirements.txt` be copied before the application code?

**Answer:**

Because Docker can cache the dependency installation layer.

If only the application code changes, Docker reuses the cached dependencies and avoids reinstalling packages.

---

# 24. Why does Docker use layers?

**Answer:**

Layers enable efficient caching, faster builds, and reuse across multiple images.

---

# 25. Why are Docker Images immutable?

**Answer:**

Immutability ensures consistency, versioning, and easy rollback to previous image versions.

---

# 26. Can one Docker Image create multiple containers?

**Answer:**

Yes.

A single Docker Image can be used to create multiple independent containers.

---

# 27. Why did Docker show a container name conflict?

**Answer:**

Container names must be unique on a Docker host.

---

# 28. What happens if the main process exits?

**Answer:**

Docker automatically stops the container because it monitors the main process.

---

# 29. Why is Docker Cache important?

**Answer:**

Docker Cache significantly reduces build time by reusing unchanged layers.

---

# 30. Explain the Docker Image lifecycle.

```
Dockerfile
      │
docker build
      │
Docker Image
      │
docker run
      │
Docker Container
```

---

# ⭐ Key Interview Tips

- Understand Dockerfile instructions instead of memorizing them.
- Explain Docker Cache with examples.
- Know the difference between RUN and CMD.
- Understand Build Context and `.dockerignore`.
- Explain Image vs Container.
- Explain why containers stop when the main process exits.
- Explain why COPY is preferred over ADD.

---

# Final Revision Checklist

- [ ] Dockerfile
- [ ] FROM
- [ ] COPY
- [ ] EXPOSE
- [ ] CMD
- [ ] RUN
- [ ] WORKDIR
- [ ] Docker Layers
- [ ] Docker Cache
- [ ] Image Immutability
- [ ] Build Context
- [ ] .dockerignore
- [ ] COPY vs ADD
- [ ] Image vs Container
- [ ] docker build
- [ ] docker run
- [ ] docker pull
