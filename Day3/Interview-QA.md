# Day 3 - Docker Internals Interview Questions and Answers

## Q1. What are Linux Namespaces?

Linux namespaces are kernel features that provide isolated views of system resources such as processes, networking, hostnames, and filesystems.

Docker uses namespaces to isolate containers from each other even though they share the same host operating system kernel.

---

## Q2. What is the difference between Namespaces and cgroups?

### Namespaces

Provide isolation.

Examples:

* Process isolation
* Network isolation
* Filesystem isolation
* Hostname isolation

### cgroups

Provide resource control.

Examples:

* CPU limits
* Memory limits
* Disk I/O limits

### Interview Summary

```text
Namespaces = Isolation
cgroups = Resource Control
```

---

## Q3. Why does `ps aux` inside a container show only a few processes?

Docker uses PID Namespace to isolate processes.

When we execute:

```bash
docker run -it ubuntu bash
ps aux
```

the container can only see processes that belong to its own PID namespace.

Processes from the host machine and other containers remain hidden.

---

## Q4. What is PID Namespace?

PID Namespace provides process isolation.

Every container receives its own process tree.

Inside a container:

```text
PID 1
```

represents the main process of that container.

If PID 1 exits or crashes, the container stops.

---

## Q5. How do containers get different IP addresses on the same host?

Docker uses Network Namespace.

Each container receives:

* Its own IP address
* Its own network interfaces
* Its own routing table
* Its own network stack

This allows multiple containers to run independently on the same host.

---

## Q6. What would happen if Docker did not use Network Namespace?

Without Network Namespace:

* IP address conflicts would occur
* Routing conflicts would occur
* Containers could interfere with each other
* Network communication would become unreliable

Network isolation would not exist.

---

## Q7. One container consumes excessive CPU and Memory. How is it controlled?

Linux cgroups are responsible for controlling resource consumption.

cgroups can limit:

* CPU usage
* Memory usage
* Disk I/O
* Network resources

Example:

```bash
docker run -m 512m nginx
```

This limits the container to 512 MB memory.

---

## Q8. Why are containers lightweight compared to virtual machines?

Containers are lightweight because:

* They do not contain a full operating system
* They share the host operating system kernel
* They start application processes directly

Virtual machines must boot a complete operating system, which requires more memory, storage, and startup time.

---

## Q9. Are containers lightweight virtual machines?

No.

Containers are not virtual machines.

### Virtual Machines

* Include full operating systems
* Have their own kernel
* Require more resources

### Containers

* Share host kernel
* Run isolated processes
* Use fewer resources

### Interview Answer

```text
Containers are isolated processes, not lightweight virtual machines.
```

---

## Q10. Why can't Container A see Container B's resources?

Docker uses different namespaces to isolate resources.

### PID Namespace

Prevents access to processes from other containers.

### Mount Namespace

Prevents access to filesystems from other containers.

### UTS Namespace

Provides hostname isolation.

### Network Namespace

Provides network isolation.

As a result, containers cannot directly access each other's resources.

---

# Bonus Question

## Why does a Kubernetes Pod enter CrashLoopBackOff?

CrashLoopBackOff occurs when the main application process inside a container repeatedly exits or crashes.

Container lifecycle depends on the main process.

Flow:

```text
Container Starts
      ↓
Main Process Crashes
      ↓
Container Stops
      ↓
Kubernetes Restarts Container
      ↓
Process Crashes Again
      ↓
CrashLoopBackOff
```

### Important Concept

A container remains alive only while its main process is running.

If the main process exits, the container stops.

---

# Frequently Asked Interview One-Liners

### What provides isolation in Docker?

Linux Namespaces.

---

### What provides resource control in Docker?

Linux cgroups.

---

### What is PID 1 inside a container?

The main process running inside the container.

---

### Why are containers lightweight?

They share the host operating system kernel.

---

### What is the purpose of Network Namespace?

To provide separate networking for each container.

---

### What is the purpose of Mount Namespace?

To provide filesystem isolation.

---

### What is the purpose of UTS Namespace?

To provide hostname isolation.

---

### What is the purpose of cgroups?

To limit and control resource usage.

---

### Are containers virtual machines?

No. Containers are isolated processes.

---

### What happens if the main process crashes?

The container stops.
