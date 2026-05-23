# Day 1 - Docker Introduction

## What is Docker?

Docker is a containerization platform used to package applications along with their dependencies, libraries, and runtime into isolated environments called containers.

Docker helps applications run consistently across different environments such as:
- Development
- Testing
- Production

---

# Why Docker Was Created?

Before Docker, developers commonly faced environment-related issues.

Example:
- Application works on developer laptop
- Fails in testing server
- Fails in production

This happened because:
- Different dependency versions
- Missing libraries
- Runtime mismatches
- OS differences

Docker solves this problem by packaging everything required for the application into a container.

---

# What is a Container?

A container is an isolated environment used to run applications.

A container contains:
- Application code
- Dependencies
- Libraries
- Runtime

Containers share the host operating system kernel, which makes them lightweight and fast.

---

# Virtual Machine vs Container

## Virtual Machine Architecture

Application  
Guest OS  
Hypervisor  
Host OS  
Hardware  

### Characteristics
- Contains full operating system
- Heavyweight
- Slow startup
- Consumes more memory and storage

---

## Container Architecture

Application  
Libraries  
Container Runtime  
Host OS Kernel  
Hardware  

### Characteristics
- Shares host OS kernel
- Lightweight
- Fast startup
- Efficient resource usage

---

# Docker Architecture

Docker architecture mainly contains:

## 1. Docker Client
The user interacts with Docker using commands like:

```bash
docker run nginx
```

The Docker client sends requests to Docker daemon.

---

## 2. Docker Daemon

Docker daemon is a background service responsible for:
- Managing containers
- Managing images
- Managing networks
- Managing volumes

Docker daemon performs the actual Docker operations.

---

## 3. Docker Registry

Docker registry stores Docker images.

Example:
- Docker Hub

If an image is not available locally, Docker pulls it from the registry.

---

# Docker Image vs Docker Container

## Docker Image

Docker image is a read-only template containing:
- Application code
- Dependencies
- Libraries
- Runtime configuration

Image is used to create containers.

---

## Docker Container

Docker container is a running instance of a Docker image.

Containers are created using Docker images.

Example:

```bash
docker run nginx
```

---

# What Happens Internally During docker run hello-world?

## Step-by-Step Workflow

1. Docker client receives command
2. Docker client sends request to Docker daemon
3. Docker daemon checks local image availability
4. If image not available, Docker pulls image from Docker Hub
5. Docker creates container from image
6. Container process starts
7. Application runs inside container
8. Container exits after main process finishes

---

# Commands Practiced

## Check Docker Version

```bash
docker --version
```

## Check Docker Service Status

```bash
systemctl status docker
```

## Run First Container

```bash
docker run hello-world
```

## View Docker Images

```bash
docker images
```

---

# Key Learnings

- Docker solves environment consistency issues
- Containers are lightweight because they share host OS kernel
- Docker image is a template
- Docker container is a running instance of image
- Docker daemon manages Docker operations
- Containers run as isolated processes

---

# Important Concepts

## Container != Virtual Machine

Container is not a mini virtual machine.

Container is an isolated process running on the host operating system.

---

# Common Mistakes Corrected

## Incorrect Understanding
Container contains its own kernel.

## Correct Understanding
Containers share the host operating system kernel.

---

## Incorrect Understanding
Container deletes automatically after execution.

## Correct Understanding
Container stops after main process exits unless removed explicitly.

---

# Real-World Usage of Docker

Docker is widely used for:
- CI/CD pipelines
- Microservices architecture
- Cloud-native applications
- Kubernetes deployments
- Consistent software delivery

---

# Conclusion

Docker provides a lightweight and consistent way to package and run applications across multiple environments. It improves deployment reliability, portability, scalability, and development efficiency.
