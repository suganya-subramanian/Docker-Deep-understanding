# Docker Day 1 - Interview Questions and Answers

## Q1. What problem does Docker solve?

Docker solves environment consistency problems by packaging applications with dependencies, libraries, and runtime into containers so applications behave consistently across environments.

---

## Q2. Difference between Docker Image and Docker Container?

### Docker Image
A read-only template containing:
- application code
- dependencies
- libraries
- runtime

### Docker Container
A running instance of a Docker image.

---

## Q3. Why are containers lightweight?

Containers are lightweight because they do not contain a full operating system. Instead, they share the host OS kernel and only package the application and required dependencies.

---

## Q4. What happens internally during docker run hello-world?

1. Docker client receives command
2. Client communicates with Docker daemon
3. Daemon checks local image
4. Pulls image if unavailable
5. Creates container
6. Starts container process
7. Application executes
8. Container exits after main process finishes

---

## Q5. What is Docker daemon?

Docker daemon is a background service responsible for managing:
- containers
- images
- networks
- volumes

It performs Docker operations internally.

---

## Q6. How does Docker solve "works on my machine" problem?

Docker packages application code, dependencies, libraries, and runtime together into containers, ensuring consistent behavior across development, testing, and production environments.

---

## Q7. What happens if internet is unavailable during docker run nginx?

- If image already exists locally → container runs successfully
- If image does not exist locally → Docker cannot pull image from registry, so container creation fails

---

## Q8. Why does hello-world container exit immediately?

The container exits because its main process finishes execution. Containers remain active only while the main process is running.

---

## Q9. Does shared kernel mean containers are not isolated?

No. Containers still remain isolated using Linux namespaces and cgroups even though they share the host OS kernel.

---

## Q10. Can containers have their own operating system?

Containers may contain user-space libraries and tools, but they do not contain a separate kernel. They share the host operating system kernel.

---

## Q11. What actually runs inside a container?

Containers run isolated processes.

---

## Q12. Which component creates containers?

Docker daemon creates containers after receiving requests from Docker client.

---

## Q13. What happens if Docker daemon stops?

Existing running containers may continue temporarily, but Docker management operations stop working until the daemon restarts.

---

## Q14. Why does Docker need images?

Docker images provide reusable, consistent templates containing application code, dependencies, libraries, and runtime configuration used to create containers.

---

## Q15. Why do containers start faster than VMs?

Containers start faster because they do not boot a full operating system. They simply start isolated application processes while sharing the host OS kernel.
