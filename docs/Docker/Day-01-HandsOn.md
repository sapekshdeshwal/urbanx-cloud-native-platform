# Docker Day 1 - Hands-on Lab

## Check Docker Version

```bash
docker --version
```

---

## Check Docker Information

```bash
docker info
```

---

## Download Nginx Image

```bash
docker pull nginx
```

---

## List Images

```bash
docker images
```

---

## Run Nginx Container

```bash
docker run -d --name my-nginx -p 8080:80 nginx
```

---

## Check Running Containers

```bash
docker ps
```

---

## Check All Containers

```bash
docker ps -a
```

---

## Stop Container

```bash
docker stop my-nginx
```

---

## Start Container

```bash
docker start my-nginx
```

---

## Restart Container

```bash
docker restart my-nginx
```

---

## View Logs

```bash
docker logs my-nginx
```

---

## Enter Running Container

```bash
docker exec -it my-nginx bash
```

---

## Check Current Directory

```bash
pwd
```

---

## Navigate to Default Website

```bash
cd /usr/share/nginx/html
```

---

## List Files

```bash
ls
```

---

## View Website HTML

```bash
cat index.html
```

---

## Exit Container

```bash
exit
```