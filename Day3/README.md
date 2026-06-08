# Day 3 - Docker Internals (Namespaces and cgroups)

## Introduction

Docker containers provide process isolation and resource control using Linux kernel features. Understanding these concepts helps explain how containers can run securely and efficiently on the same host operating system.

This day focused on:

* Linux Namespaces
* cgroups
* Process Isolation
* Network Isolation
* Filesystem Isolation
* Hostname Isolation
* Why Containers Are Lightweight

---

# Linux Namespaces

## What are Namespaces?

Linux namespaces are kernel features that provide isolated views of system resources.

Docker uses namespaces to ensure that containers are isolated from each other even though they share the same host operating system kernel.

Without namespaces, containers would be able to see and interfere with each other's resources.

---

# Types of Namespaces

## 1. PID Namespace (Process Isolation)

PID stands for Process ID.

PID namespace allows a container to view only its own processes.

### Example

Inside a container:

```bash
ps aux
```

Only container-specific processes are displayed.

Processes running on the host or in other containers are hidden.

### Important Concept

The main process inside a container becomes:

```text
PID 1
```

within that container's namespace.

If PID 1 exits, the container stops.

---

## 2. Network Namespace

Network namespace provides network isolation.

Each container gets:

* Separate IP address
* Separate network interfaces
* Separate routing table
* Separate network stack

### Example

```bash
docker inspect <container-id>
```

Different containers receive different IP addresses.

### Benefits

* Avoids IP conflicts
* Isolates network communication
* Improves security

---

## 3. Mount Namespace (Filesystem Isolation)

Mount namespace provides filesystem isolation.

Each container receives its own view of the filesystem.

### Benefits

* Containers cannot directly access files from other containers
* Improves security
* Prevents accidental modification of files

---

## 4. UTS Namespace (Hostname Isolation)

UTS namespace isolates hostname information.

### Example

Inside a container:

```bash
hostname
```

The container displays its own hostname rather than the host machine hostname.

### Benefits

* Unique container identification
* Improved isolation

---

# What are cgroups?

cgroups (Control Groups) are Linux kernel features used to manage and limit resource usage.

While namespaces provide isolation, cgroups provide resource control.

---

# Resources Controlled by cgroups

* CPU
* Memory
* Disk I/O
* Network resources

---

# Example

Limit container memory usage:

```bash
docker run -m 512m nginx
```

This limits the container to 512 MB memory.

---

# Namespace vs cgroups

| Feature    | Purpose          |
| ---------- | ---------------- |
| Namespaces | Isolation        |
| cgroups    | Resource Control |

### Simple Understanding

Namespaces answer:

```text
Who can see what?
```

cgroups answer:

```text
How much can use what?
```

---

# Why Containers Are Lightweight

Containers are lightweight because:

* They do not include a full operating system
* They share the host OS kernel
* They start application processes directly

---

# Virtual Machine Architecture

```text
Application
Guest OS
Kernel
Hypervisor
Host OS
Hardware
```

### Characteristics

* Full operating system per VM
* Higher memory usage
* Larger storage requirements
* Slower startup

---

# Container Architecture

```text
Application
Libraries
Container Runtime
Host OS Kernel
Hardware
```

### Characteristics

* Shared host kernel
* Lower memory usage
* Faster startup
* Efficient resource utilization

---

# Practical Commands Executed

## Start Interactive Container

```bash
docker run -it ubuntu bash
```

---

## View Processes

```bash
ps aux
```

Observation:

Only container-specific processes are visible.

---

## View Hostname

```bash
hostname
```

Observation:

Container has its own hostname due to UTS namespace.

---

## Inspect Container

```bash
docker inspect <container-id>
```

Observation:

Container receives its own IP address through network namespace.

---

## Apply Memory Limit

```bash
docker run -m 512m nginx
```

Observation:

Memory usage is controlled using cgroups.

---

# Key Learnings

* Containers are isolated using Linux namespaces.
* PID namespace isolates processes.
* Network namespace isolates networking resources.
* Mount namespace isolates filesystems.
* UTS namespace isolates hostnames.
* cgroups control resource consumption.
* Containers share the host operating system kernel.
* Containers are isolated processes, not virtual machines.

---

# Important Interview Concepts

## Namespaces

Provide isolation.

---

## cgroups

Provide resource control.

---

## PID Namespace

Allows containers to see only their own processes.

---

## Network Namespace

Provides separate network stack and IP address.

---

## Mount Namespace

Provides filesystem isolation.

---

## UTS Namespace

Provides hostname isolation.

---

## Container Lifecycle

Container remains alive only while its main process is running.

---

# Common Mistakes Corrected

## Incorrect

Containers contain their own kernel.

## Correct

Containers share the host operating system kernel.

---

## Incorrect

Containers are lightweight virtual machines.

## Correct

Containers are isolated processes running on a shared kernel.

---

# Real-World Usage

These concepts are heavily used in:

* Docker
* Kubernetes
* OpenShift
* Container Platforms
* Cloud Native Applications

Understanding namespaces and cgroups helps troubleshoot:

* Container crashes
* Resource exhaustion
* CPU bottlenecks
* Memory issues
* Kubernetes Pod failures

---

# Conclusion

Linux namespaces and cgroups form the foundation of container technology. Namespaces provide isolation, while cgroups provide resource control. Together they enable Docker containers to run securely, efficiently, and independently on the same host operating system.
