# Docker Day 3 - Hands-On

## Practical 1 - Docker Volume

### Create Volume

```bash
docker volume create postgres-data
```

### Verify

```bash
docker volume ls
```

---

## Practical 2 - Persistent Storage

Run Ubuntu

```bash
docker run -it \
--name ubuntu-volume-test \
-v postgres-data:/data \
ubuntu bash
```

Inside Container

```bash
cd /data

echo "Hello Sapeksh" > message.txt

cat message.txt
```

Delete Container

```bash
docker rm ubuntu-volume-test
```

Create Another Container

```bash
docker run -it \
--name ubuntu-volume-test-2 \
-v postgres-data:/data \
ubuntu bash
```

Verify

```bash
cd /data

cat message.txt
```

Result:

Data still exists.

---

## Practical 3 - Docker Network

List Networks

```bash
docker network ls
```

Create Network

```bash
docker network create urbanx-network
```

Run Frontend

```bash
docker run -dit \
--name frontend \
--network urbanx-network \
ubuntu bash
```

Run Backend

```bash
docker run -dit \
--name backend \
--network urbanx-network \
ubuntu bash
```

Install Ping

```bash
apt update

apt install -y iputils-ping
```

Ping Backend

```bash
ping backend
```

---

## Practical 4 - Docker Inspect

```bash
docker inspect frontend
```

Observe:

- NetworkMode
- Image
- IPAddress
- DNSNames

---

## Practical 5 - Docker Logs

Run Nginx

```bash
docker run -d \
--name nginx-demo \
--network urbanx-network \
-p 8085:80 \
nginx
```

View Logs

```bash
docker logs nginx-demo
```

Live Logs

```bash
docker logs -f nginx-demo
```