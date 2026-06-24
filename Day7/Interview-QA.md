# Day 7 - Docker Networking Interview Questions & Answers

## Q1. Why do containers need Docker networking?

Docker networking enables communication between containers, host machines, and external services.

Example:

```text
Frontend
    ↓
Backend
    ↓
MySQL
```

Without networking, these services cannot communicate.

---

## Q2. What is a Bridge Network?

Bridge network is Docker's default network driver.

When a container is created without specifying a network, Docker automatically attaches it to the bridge network.

Example:

```bash
docker run nginx
```

---

## Q3. Explain:

```bash
docker run -p 8080:80 nginx
```

### Host Port

```text
8080
```

### Container Port

```text
80
```

Flow:

```text
Host Port 8080
      ↓
Container Port 80
      ↓
Nginx Application
```

---

## Q4. Can containers communicate without port mapping?

Yes.

Containers on the same Docker network can communicate directly using container IPs or container names.

Port mapping is only required for host-to-container access.

---

## Q5. Why use Custom Bridge Networks?

Benefits:

* Better isolation
* Built-in DNS resolution
* Easier service discovery
* Production-ready networking

---

## Q6. What is Docker DNS?

Docker DNS automatically resolves container names into IP addresses.

Example:

```text
mysql
     ↓
172.19.0.3
```

Applications can use:

```text
mysql:3306
```

instead of IP addresses.

---

## Q7. Which is better in production?

### Container Name

Preferred.

### Why?

* IP addresses change
* Names remain stable
* Docker DNS handles resolution automatically

---

## Q8. Difference between Bridge and Host Network

### Bridge Network

* Separate container IP
* Better isolation
* Port mapping often required

### Host Network

* Uses host network directly
* No separate container IP
* No port mapping required

---

## Q9. What happens with None Network?

Example:

```bash
docker run --network none ubuntu
```

Result:

* No Internet access
* No container communication
* No external connectivity

---

## Q10. How would you troubleshoot container communication issues?

### Step 1

Verify containers are running:

```bash
docker ps
```

### Step 2

Verify network membership:

```bash
docker network inspect demo-net
```

### Step 3

Verify same network

### Step 4

Verify DNS resolution:

```bash
getent hosts mysql
```

### Step 5

Verify application configuration

### Step 6

Check container logs:

```bash
docker logs <container>
```

---

# Bonus Question

## Why is using container IP addresses a bad practice?

Container IPs can change when containers are recreated.

Example:

```text
Old IP → 172.19.0.2

New IP → 172.19.0.10
```

Applications depending on old IP addresses will fail.

---

## How does Docker solve this problem?

Docker provides DNS-based service discovery.

Applications communicate using:

```text
Container Names
```

instead of IP addresses.

---

# Frequently Asked One-Liners

### What is Docker's default network?

Bridge Network.

---

### What does Port Mapping do?

Exposes container ports to the host machine.

---

### What does 8080:80 mean?

```text
HostPort:ContainerPort
```

---

### Do containers on the same network need port mapping?

No.

---

### What is Docker DNS?

Container name resolution service.

---

### Which network type provides no networking?

None Network.

---

### Which network type uses host networking directly?

Host Network.

---

### Which network type is recommended for production microservices?

Custom Bridge Network.

---

### Why use container names instead of IPs?

Container names remain stable while IPs can change.

---

### Golden Interview Answer

Containers on the same Docker network can communicate directly without port mapping.

---

### Second Golden Interview Answer

Port mapping is required only when the host machine needs access to the container.
