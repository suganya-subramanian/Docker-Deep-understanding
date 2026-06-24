# Day 7 - Docker Networking

## Introduction

Docker Networking enables communication between containers, host machines, and external services. Modern applications are typically composed of multiple containers such as frontend, backend, databases, and cache servers. Docker networking allows these services to communicate securely and efficiently.

---

# Why Docker Networking?

Consider a three-tier application:

```text
Frontend Container
        ↓
Backend Container
        ↓
MySQL Container
```

The frontend must communicate with the backend, and the backend must communicate with the database.

Without Docker networking, container-to-container communication would not be possible.

---

# Docker Network Types

Docker provides three default network types:

1. Bridge Network
2. Host Network
3. None Network

View available networks:

```bash
docker network ls
```

---

# Bridge Network

Bridge is the default Docker network.

Example:

```bash
docker run -d nginx
```

Docker automatically attaches the container to the bridge network.

### Characteristics

* Default Docker network
* Each container gets its own IP address
* Containers can communicate on the same bridge network
* Provides network isolation

### Example

```text
Container A
      ↓
Bridge Network
      ↓
Container B
```

---

# Inspect Bridge Network

```bash
docker network inspect bridge
```

Useful information:

* Connected containers
* Subnet
* Gateway
* Network configuration

---

# Container IP Addresses

Each container receives a unique IP address.

Example:

```text
web1 → 172.17.0.2
web2 → 172.17.0.3
```

These IPs are internal to Docker.

---

# Port Mapping

Port mapping allows external users to access applications running inside containers.

Example:

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host Port 8080
        ↓
Container Port 80
```

### Flow

```text
Browser
     ↓
localhost:8080
     ↓
Docker Port Mapping
     ↓
Container Port 80
     ↓
Nginx Application
```

---

# Host Network

Host network allows a container to use the host machine's network directly.

Example:

```bash
docker run --network host nginx
```

### Characteristics

* No separate container IP
* Uses host network directly
* Better performance
* No port mapping required

### Disadvantages

* Reduced isolation
* Possible port conflicts

---

# None Network

None network disables networking completely.

Example:

```bash
docker run --network none ubuntu
```

### Characteristics

* No Internet access
* No container communication
* No external connectivity

### Use Cases

* Security testing
* Offline workloads
* Isolated environments

---

# Custom Bridge Network

Create a custom network:

```bash
docker network create demo-net
```

Run containers:

```bash
docker run -dit --name c1 --network demo-net ubuntu

docker run -dit --name c2 --network demo-net ubuntu
```

---

# Benefits of Custom Networks

* Better isolation
* Built-in DNS resolution
* Easier service discovery
* Production-ready architecture

---

# Docker DNS Resolution

Custom networks provide automatic DNS resolution.

Example:

```text
Container Name = mysql
```

Application can connect using:

```text
mysql:3306
```

instead of:

```text
172.19.0.3:3306
```

Docker automatically resolves:

```text
mysql
      ↓
172.19.0.3
```

---

# Why Container Names Are Better Than IP Addresses

Container IP addresses can change when containers are recreated.

Example:

```text
Old IP → 172.19.0.2

New IP → 172.19.0.10
```

Container names remain the same.

Docker DNS automatically maps names to current IP addresses.

---

# Practical Lab

Create network:

```bash
docker network create demo-net
```

Run containers:

```bash
docker run -dit --name c1 --network demo-net ubuntu

docker run -dit --name c2 --network demo-net ubuntu
```

Inspect network:

```bash
docker network inspect demo-net
```

Observed:

```text
c1 → 172.19.0.2

c2 → 172.19.0.3
```

Both containers were successfully connected to the same network.

---

# Important Commands

```bash
docker network ls

docker network inspect bridge

docker network inspect demo-net

docker network create demo-net

docker run -d nginx

docker run -d -p 8080:80 nginx

docker run --network host nginx

docker run --network none ubuntu
```

---

# Troubleshooting Container Communication

If Application Container cannot connect to Database Container:

1. Verify containers are running

```bash
docker ps
```

2. Verify network membership

```bash
docker network inspect demo-net
```

3. Verify both containers are in same network

4. Verify DNS resolution

```bash
getent hosts mysql
```

5. Verify application configuration

```text
MYSQL_HOST=mysql
```

6. Check container logs

```bash
docker logs <container>
```

---

# Key Learnings

* Docker networking enables container communication.
* Bridge network is Docker's default network.
* Port mapping exposes container ports to host machine.
* Host network shares host networking directly.
* None network disables networking.
* Custom networks provide built-in DNS.
* Container names should be preferred over IP addresses.
* Containers on the same network communicate without port mapping.

---

# Conclusion

Docker networking is a fundamental component of containerized applications. Understanding bridge networks, host networks, none networks, port mapping, custom networks, and Docker DNS is essential for Docker, Kubernetes, and DevOps engineering.
