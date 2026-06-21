# Day 6 - ENTRYPOINT, CMD Overrides and Container Startup Flow

## Introduction

Docker provides two important instructions for defining container startup behavior:

* CMD
* ENTRYPOINT

Understanding these instructions is essential because they control how containers start and how commands can be customized at runtime.

This topic is frequently asked in Docker and DevOps interviews.

---

# What is CMD?

CMD defines the default command that executes when a container starts.

Example:

```Dockerfile
CMD ["echo", "Hello Docker"]
```

When container starts:

```bash
echo "Hello Docker"
```

is executed.

---

# Characteristics of CMD

* Executes during container runtime
* Defines default command
* Can be overridden
* Used to provide default behavior

---

# CMD Override Example

Dockerfile:

```Dockerfile
CMD ["echo", "Hello"]
```

Run:

```bash
docker run my-image
```

Output:

```text
Hello
```

Run:

```bash
docker run my-image ls
```

Output:

```text
Directory listing
```

The CMD instruction is completely replaced by the new command.

---

# What is ENTRYPOINT?

ENTRYPOINT defines the main executable that always runs when the container starts.

Example:

```Dockerfile
ENTRYPOINT ["echo"]
```

Run:

```bash
docker run my-image Suganya
```

Docker executes:

```bash
echo Suganya
```

Output:

```text
Suganya
```

---

# Characteristics of ENTRYPOINT

* Defines the primary executable
* Usually remains fixed
* Arguments can be passed during runtime
* Useful for utility-style containers

---

# CMD vs ENTRYPOINT

| CMD                   | ENTRYPOINT                 |
| --------------------- | -------------------------- |
| Default command       | Main executable            |
| Easily overridden     | Usually fixed              |
| Runtime configuration | Runtime execution          |
| Optional              | Defines container behavior |

---

# Key Difference

```text
ENTRYPOINT = Fixed Executable

CMD = Default Arguments
```

---

# Using ENTRYPOINT and CMD Together

This is the most common production pattern.

Example:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Docker combines them internally:

```bash
python app.py
```

---

# Override Example

Run:

```bash
docker run my-image
```

Executes:

```bash
python app.py
```

Run:

```bash
docker run my-image test.py
```

Executes:

```bash
python test.py
```

CMD is replaced.

ENTRYPOINT remains unchanged.

---

# ENTRYPOINT Override

ENTRYPOINT can be overridden using:

```bash
docker run --entrypoint bash my-image
```

Docker ignores the original ENTRYPOINT and starts:

```bash
bash
```

instead.

---

# Container Startup Flow

Dockerfile:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Container startup sequence:

```text
Image
 ↓
Container Created
 ↓
ENTRYPOINT Loaded
 ↓
CMD Loaded
 ↓
Commands Combined
 ↓
Main Process Starts
```

Final command:

```bash
python app.py
```

---

# Why Containers Stop

A container remains alive only while its main process is running.

Example:

```Dockerfile
CMD ["echo", "Hello"]
```

Execution:

```text
Container Starts
      ↓
Prints Hello
      ↓
Process Ends
      ↓
Container Stops
```

---

# Multiple CMD Instructions

Dockerfile:

```Dockerfile
CMD ["First"]

CMD ["Second"]
```

Only the last CMD instruction is used.

Result:

```text
Second
```

---

# Multiple ENTRYPOINT Instructions

Dockerfile:

```Dockerfile
ENTRYPOINT ["echo"]

ENTRYPOINT ["python"]
```

Only the last ENTRYPOINT instruction is used.

Result:

```text
python
```

---

# Practical Examples

## CMD Only

```Dockerfile
FROM ubuntu

CMD ["echo", "Hello"]
```

---

## ENTRYPOINT Only

```Dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]
```

---

## ENTRYPOINT + CMD

```Dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]

CMD ["Docker"]
```

Run:

```bash
docker run image
```

Output:

```text
Docker
```

Run:

```bash
docker run image Suganya
```

Output:

```text
Suganya
```

---

# Commands Practiced

```bash
docker run image

docker run image ls

docker run --entrypoint bash image

docker build -t my-image .
```

---

# Key Learnings

* CMD defines default runtime command.
* ENTRYPOINT defines the main executable.
* CMD can be overridden.
* ENTRYPOINT usually remains fixed.
* ENTRYPOINT and CMD can be combined.
* Container lifecycle depends on the main process.
* Only the last CMD instruction is used.
* Only the last ENTRYPOINT instruction is used.

---

# Conclusion

ENTRYPOINT and CMD are essential Dockerfile instructions that control container startup behavior. Understanding their differences, override behavior, and combined usage is critical for designing flexible and production-ready Docker images.
