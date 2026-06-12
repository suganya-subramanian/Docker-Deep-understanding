# Day 4 - Docker Images, Layers and Image Internals

## Introduction

Docker images are the foundation of container technology. Every container is created from an image. Understanding image layers, copy-on-write, tags, and image storage optimization is essential for Docker, Kubernetes, and DevOps engineering.

---

# What is a Docker Image?

A Docker image is a read-only layered template used to create containers.

A Docker image contains:

* Application Code
* Runtime
* Libraries
* Dependencies
* Configuration Files

Docker images are immutable and reusable.

---

# Docker Image vs Docker Container

## Docker Image

* Read-only template
* Contains application and dependencies
* Used to create containers
* Reusable

## Docker Container

* Running instance of an image
* Contains writable layer
* Can be started, stopped, and deleted

### Relationship

```text
Docker Image
      ↓
Docker Container
```

---

# Docker Image Layers

Docker images are built using multiple layers.

Example:

```text
Ubuntu Base Layer
      ↓
Python Layer
      ↓
Application Layer
      ↓
Configuration Layer
```

Together these layers form a complete image.

---

# Why Docker Uses Layers

Docker uses layers for:

* Storage efficiency
* Layer reuse
* Faster downloads
* Faster builds
* Reduced disk usage

---

# Layer Reuse Example

Image A

```text
Ubuntu
Python
App-A
```

Image B

```text
Ubuntu
Python
App-B
```

Docker stores:

```text
Ubuntu
Python
```

only once.

Only application-specific layers are stored separately.

This reduces storage consumption.

---

# Docker Image History

View image layer history:

```bash
docker history nginx
```

This command displays:

* Layer history
* Commands used to build image
* Layer sizes
* Build sequence

---

# Why Docker Images Are Read-Only

Docker images are shared by multiple containers.

If images were writable:

* Containers could modify shared files
* Other containers could be affected
* Image consistency would be lost

Therefore Docker images remain read-only.

---

# Writable Container Layer

When a container is created, Docker adds a writable layer above image layers.

```text
Read-Only Image Layers
           +
Writable Container Layer
           =
Docker Container
```

---

# Copy-on-Write (CoW)

Docker uses Copy-on-Write technology.

When a container modifies a file:

1. Docker copies the file from image layer
2. File is placed into writable layer
3. Modification occurs in writable layer

The original image remains unchanged.

---

# Copy-on-Write Example

Image contains:

```text
/app/config.txt
```

Container A modifies file.

Result:

```text
Container A
    ↓
Writable Layer Modified
```

Container B still sees the original file.

This ensures isolation and image consistency.

---

# Image ID

Every image has a unique Image ID.

View images:

```bash
docker images
```

Image ID uniquely identifies image contents.

Images with identical contents can share the same Image ID.

---

# Docker Tags

Tags are labels used to identify image versions.

Examples:

```text
latest
1.27
stable
dev
```

Example:

```bash
docker pull nginx:latest
docker pull nginx:1.27
```

---

# Is Latest Always the Newest Version?

No.

The latest tag is simply a tag name.

It points to whichever version the image maintainer chooses.

```text
latest ≠ always newest version
```

---

# Alpine vs Ubuntu Images

## Ubuntu

Advantages:

* More tools available
* Easier for beginners

Disadvantages:

* Larger image size
* Slower downloads

---

## Alpine

Advantages:

* Very small image size
* Faster image pull
* Faster deployments
* Lower storage usage
* Smaller attack surface

Disadvantages:

* Fewer built-in utilities

---

# Why Smaller Images Matter

Smaller images provide:

* Faster image pull
* Faster image push
* Faster deployments
* Faster CI/CD pipelines
* Faster Kubernetes Pod startup
* Reduced storage requirements
* Reduced bandwidth consumption

---

# Commands Practiced

```bash
docker images

docker image ls

docker history nginx

docker history ubuntu

docker pull alpine

docker inspect nginx
```

---

# Key Learnings

* Docker images are read-only templates.
* Containers are created from images.
* Images are composed of multiple layers.
* Docker uses layer reuse for storage optimization.
* Containers contain writable layers.
* Docker uses Copy-on-Write for file modifications.
* Alpine images are preferred for lightweight deployments.
* Smaller images improve CI/CD and Kubernetes performance.

---

# Real-World Usage

Understanding image layers helps with:

* Dockerfile optimization
* CI/CD pipeline optimization
* Kubernetes deployments
* Faster image distribution
* Production troubleshooting

---

# Conclusion

Docker images form the foundation of containerized applications. Features such as layers, Copy-on-Write, and image reuse make Docker efficient, scalable, and suitable for modern DevOps and cloud-native environments.

