# Day 2 - Docker Core Commands and Container Lifecycle

# Introduction

Day 2 focused on understanding Docker container lifecycle, container execution behavior, foreground and detached modes, interactive containers, logs, and container management commands.

This day is very important because it explains how containers actually behave internally.

---

# Docker Container Lifecycle

Docker containers follow a lifecycle model:

Created → Running → Stopped → Removed

---

## Created

Container exists but is not running yet.

---

## Running

The main process inside the container is active.

---

## Stopped

The container stops when:
- main process exits
- container is manually stopped
- application crashes

---

## Removed

The container is completely deleted from the system.

---

# Important Concept

A container remains alive only while its main foreground process is running.

If the main process exits, the container stops automatically.

---

# Example: Ubuntu vs Nginx Container Behavior

## Ubuntu Container

```bash
docker run ubuntu
```

The container exits immediately because no long-running foreground process is started by default.

---

## Nginx Container

```bash
docker run nginx
```

The container continues running because nginx starts a continuous foreground web server process.

---

# Foreground Mode vs Detached Mode

## Foreground Mode

```bash
docker run nginx
```

- Terminal becomes attached to container process
- Terminal remains blocked while container runs

---

## Detached Mode

```bash
docker run -d nginx
```

### -d Flag
Detached mode runs container in background.

Benefits:
- terminal becomes free
- useful in production environments

---

# Docker Commands Practiced

# View Running Containers

```bash
docker ps
```

Displays only running containers.

---

# View All Containers

```bash
docker ps -a
```

Displays:
- running containers
- stopped containers
- exited containers

---

# Run Container

```bash
docker run nginx
```

docker run performs:
- container creation
- container startup

---

# Run Container in Detached Mode

```bash
docker run -d nginx
```

---

# Run Interactive Container

```bash
docker run -it ubuntu bash
```

### -i
Interactive mode

### -t
Terminal mode

### bash
Starts bash shell inside container

---

# Important Understanding

The bash shell becomes the main process inside the container.

When bash exits, the container also exits.

---

# Stop Container

```bash
docker stop <container-id>
```

Docker sends SIGTERM signal for graceful shutdown.

---

# Kill Container

```bash
docker kill <container-id>
```

Docker sends SIGKILL signal for immediate termination.

---

# Difference Between docker stop and docker kill

## docker stop
- graceful shutdown
- allows application cleanup
- safer

## docker kill
- forcefully terminates process
- immediate shutdown
- may cause abrupt termination

---

# Restart Container

```bash
docker restart <container-id>
```

Equivalent to:
- stop
- start

---

# Start Stopped Container

```bash
docker start <container-id>
```

---

# Remove Container

```bash
docker rm <container-id>
```

---

# Force Remove Running Container

```bash
docker rm -f <container-id>
```

Forcefully stops and removes container.

---

# Docker Exec

```bash
docker exec -it <container-id> bash
```

Used to enter an already running container.

Important:
docker exec does NOT create a new container.

---

# Difference Between docker run and docker exec

## docker run
- creates new container
- starts container

## docker exec
- enters existing running container
- executes commands inside container

---

# Docker Logs

```bash
docker logs <container-id>
```

Used for:
- debugging
- troubleshooting
- checking application output
- identifying startup failures
- identifying crash reasons

---

# Docker Inspect

```bash
docker inspect <container-id>
```

Displays detailed container metadata in JSON format.

Useful information:
- container IP address
- mounted volumes
- environment variables
- network configuration
- port mappings

---

# Key Learnings

- Container lifecycle depends on main process
- docker run creates and starts containers
- docker exec enters running containers
- docker stop performs graceful shutdown
- docker kill forcefully terminates containers
- logs are critical for debugging
- inspect helps identify container metadata and configuration

---

# Important Concepts

## Container != Virtual Machine

Containers are isolated process environments, not full virtual machines.

---

## Main Foreground Process

Container remains alive only while its main foreground process is running.

---

# Real-World Usage

These Docker commands are widely used in:
- CI/CD pipelines
- Kubernetes troubleshooting
- production debugging
- container monitoring
- application deployment

---

# Conclusion

Understanding Docker container lifecycle and management commands is essential for working with containers in real-world DevOps environments. These concepts form the foundation for advanced Docker, Kubernetes, and production troubleshooting skills.
