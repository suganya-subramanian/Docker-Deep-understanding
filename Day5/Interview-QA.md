# Day 5 - Dockerfile Interview Questions and Answers

## Q1. What is a Dockerfile?

A Dockerfile is a text file containing instructions used to build Docker images.

It automates image creation and ensures consistency across environments.

---

## Q2. Explain Dockerfile → Build → Image → Container Flow

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

### Dockerfile

Contains build instructions.

### docker build

Reads Dockerfile and creates image.

### Docker Image

Read-only template containing application and dependencies.

### docker run

Creates and starts container from image.

### Docker Container

Running instance of image.

---

## Q3. What is the purpose of FROM?

FROM specifies the base image used to build the new image.

Example:

```Dockerfile
FROM ubuntu
```

---

## Q4. What happens if Dockerfile does not contain FROM?

Docker does not know which base image or filesystem to use.

Image build fails.

---

## Q5. Difference between RUN and CMD?

### RUN

```Dockerfile
RUN apt update
```

* Executes during image build
* Creates image layers

### CMD

```Dockerfile
CMD ["nginx"]
```

* Executes during container startup
* Defines default container command

---

## Q6. When does RUN execute?

RUN executes during image build time.

---

## Q7. When does CMD execute?

CMD executes during container runtime.

---

## Q8. Output of Dockerfile Example

Dockerfile:

```Dockerfile
FROM ubuntu

RUN echo "Build Stage"

CMD ["echo", "Container Started"]
```

### During Build

```bash
docker build -t test .
```

Output:

```text
Build Stage
```

### During Run

```bash
docker run test
```

Output:

```text
Container Started
```

---

## Q9. Can Dockerfile contain multiple RUN instructions?

Yes.

Example:

```Dockerfile
RUN apt update

RUN apt install -y nginx

RUN mkdir /app
```

Each RUN creates a new image layer.

---

## Q10. Can Dockerfile contain multiple CMD instructions?

Yes.

However:

```text
Only the last CMD instruction is used.
```

---

## Q11. What is the purpose of COPY?

COPY transfers files from local build context into Docker image.

Example:

```Dockerfile
COPY app.py /app/
```

---

## Q12. From where does COPY copy files?

COPY copies files from:

```text
Local Build Context
```

into the image.

---

## Q13. What is WORKDIR?

WORKDIR sets the default working directory inside the image.

Example:

```Dockerfile
WORKDIR /app
```

---

## Q14. What happens in:

```Dockerfile
WORKDIR /app

COPY . .
```

All files from current local directory are copied into:

```text
/app
```

inside the image.

---

## Q15. Is it a good practice to install software using CMD?

No.

Example:

```Dockerfile
CMD ["apt", "install", "-y", "nginx"]
```

Problems:

* Slow startup
* Internet dependency
* Repeated installation

Correct approach:

```Dockerfile
RUN apt install -y nginx
```

during image build.

---

## Q16. If index.html changes, will existing image update automatically?

No.

Image must be rebuilt manually.

```bash
docker build -t my-app .
```

---

## Q17. If Dockerfile changes, will Docker rebuild image automatically?

No.

Docker requires a new build command.

---

## Q18. Why are Dockerfiles preferred over manual setup?

Benefits:

1. Automation
2. Consistency
3. Reproducibility
4. Faster deployment
5. Version control
6. Reduced human error

---

## Q19. Which instruction installs software and which starts software?

### Install Software

```Dockerfile
RUN
```

Example:

```Dockerfile
RUN apt install -y nginx
```

### Start Software

```Dockerfile
CMD
```

or

```Dockerfile
ENTRYPOINT
```

---

# Bonus Question

## Container exits immediately after docker run. Which instruction would you check first?

Check:

```Dockerfile
CMD
```

or

```Dockerfile
ENTRYPOINT
```

because container lifecycle depends on the main process.

If the main process exits, the container stops.

Example:

```Dockerfile
CMD ["echo", "Hello"]
```

Container:

```text
Starts
 ↓
Prints Hello
 ↓
Exits
```

---

# Frequently Asked One-Liners

### What is a Dockerfile?

Instructions used to build Docker images.

---

### What is FROM?

Base image instruction.

---

### What is RUN?

Executes commands during build time.

---

### What is CMD?

Executes default command during runtime.

---

### What is COPY?

Copies files into image.

---

### What is WORKDIR?

Sets working directory inside image.

---

### Can Dockerfile have multiple RUN instructions?

Yes.

---

### Can Dockerfile have multiple CMD instructions?

Yes, but only the last CMD is used.

---

### RUN vs CMD?

RUN = Build Time

CMD = Runtime
