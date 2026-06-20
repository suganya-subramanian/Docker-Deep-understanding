# Day 5 - Dockerfile Fundamentals

## Introduction

A Dockerfile is a text file containing instructions used to build Docker images. It automates image creation and ensures consistency across development, testing, and production environments.

Dockerfiles are one of the most important concepts in Docker because they enable Infrastructure as Code (IaC) for containerized applications.

---

# What is a Dockerfile?

A Dockerfile is a text file containing a sequence of instructions that Docker uses to build an image.

Example:

```Dockerfile
FROM ubuntu

RUN apt update

CMD ["echo", "Hello Docker"]
```

---

# Why Do We Need Dockerfiles?

Without Dockerfiles:

* Manual software installation
* Manual configuration
* Inconsistent environments
* Time-consuming deployments

With Dockerfiles:

* Automated builds
* Consistent environments
* Faster deployments
* Version-controlled infrastructure
* Reproducible images

---

# Docker Build Workflow

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

### Step 1

Docker reads Dockerfile instructions.

### Step 2

Docker executes instructions one by one.

### Step 3

Docker creates image layers.

### Step 4

Docker builds the final image.

### Step 5

Container is created from the image.

---

# FROM Instruction

The FROM instruction specifies the base image.

Example:

```Dockerfile
FROM ubuntu
```

Meaning:

* Start image creation using Ubuntu base image.
* Acts as the foundation for the new image.

---

# Why FROM is Important

Docker requires a starting filesystem and environment.

Without FROM:

* No base image
* No filesystem
* Image build fails

---

# RUN Instruction

RUN executes commands during image build time.

Example:

```Dockerfile
RUN apt update
```

```Dockerfile
RUN apt install -y nginx
```

---

# Characteristics of RUN

* Executes during image build
* Creates new image layers
* Used for software installation
* Used for package updates

---

# CMD Instruction

CMD defines the default command executed when a container starts.

Example:

```Dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

When container starts:

```bash
nginx -g "daemon off;"
```

executes automatically.

---

# Characteristics of CMD

* Executes during container runtime
* Defines default startup command
* Can be overridden

---

# RUN vs CMD

| RUN                   | CMD                      |
| --------------------- | ------------------------ |
| Executes during build | Executes during runtime  |
| Creates image layers  | Starts container process |
| Used for installation | Used for execution       |

### Example

```Dockerfile
FROM ubuntu

RUN apt update
RUN apt install -y nginx

CMD ["nginx", "-g", "daemon off;"]
```

---

# COPY Instruction

COPY copies files from local machine into Docker image.

Example:

```Dockerfile
COPY index.html /usr/share/nginx/html/
```

Meaning:

```text
Local File
      ↓
Docker Image
```

---

# Real-World Usage of COPY

Used for:

* Application code
* Configuration files
* Scripts
* Certificates

---

# WORKDIR Instruction

WORKDIR sets the default working directory inside the image.

Example:

```Dockerfile
WORKDIR /app
```

After this:

```Dockerfile
COPY . .
```

copies files into:

```text
/app
```

---

# Benefits of WORKDIR

* Cleaner Dockerfiles
* Shorter file paths
* Easier maintenance

---

# Multiple RUN Instructions

Dockerfiles can contain multiple RUN instructions.

Example:

```Dockerfile
RUN apt update

RUN apt install -y nginx

RUN mkdir /app
```

Each RUN creates a new image layer.

---

# Multiple CMD Instructions

Dockerfiles can contain multiple CMD instructions.

However:

```text
Only the last CMD instruction is used.
```

Example:

```Dockerfile
CMD ["echo", "First"]

CMD ["echo", "Second"]
```

Output:

```text
Second
```

---

# Practical Project

## index.html

```html
<h1>Hello Suganya Docker Learning</h1>
```

---

## Dockerfile

```Dockerfile
FROM nginx

COPY index.html /usr/share/nginx/html/index.html
```

---

# Build Image

```bash
docker build -t my-web .
```

---

# Run Container

```bash
docker run -d -p 8080:80 my-web
```

---

# Commands Practiced

```bash
docker build -t my-image .

docker images

docker run my-image

docker run -d my-image

docker inspect my-image
```

---

# Key Learnings

* Dockerfile is used to build Docker images.
* FROM specifies the base image.
* RUN executes during image build.
* CMD executes during container startup.
* COPY transfers files into image.
* WORKDIR defines working directory.
* Docker images are built layer by layer.
* Only the last CMD instruction is executed.

---

# Common Mistakes Corrected

## Incorrect

RUN and CMD execute at the same time.

## Correct

RUN executes during image build.

CMD executes during container runtime.

---

## Incorrect

Docker automatically rebuilds image when files change.

## Correct

Image must be rebuilt using:

```bash
docker build
```

---

# Conclusion

Dockerfiles automate image creation and ensure consistent deployments. Understanding Dockerfile instructions such as FROM, RUN, COPY, WORKDIR, and CMD is essential for Docker, Kubernetes, and DevOps engineering.
