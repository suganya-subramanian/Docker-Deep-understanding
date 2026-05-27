# Docker Day 2 - Interview Questions and Answers

# Q1. Difference between docker run and docker exec?

## docker run
- Creates new container
- Starts container from image

## docker exec
- Executes commands inside already running container
- Does not create new container

---

# Q2. Why does docker run ubuntu exit immediately but docker run nginx keeps running?

The ubuntu container exits because no long-running foreground process is started by default.

The nginx container continues running because nginx starts a continuous foreground web server process.

---

# Q3. Difference between docker ps and docker ps -a?

## docker ps
Displays only running containers.

## docker ps -a
Displays all containers including:
- running
- stopped
- exited containers

---

# Q4. What happens internally during docker stop?

Docker sends SIGTERM signal to the main process inside the container, allowing graceful shutdown.

If process does not stop within timeout period, Docker sends SIGKILL.

---

# Q5. Difference between docker stop and docker kill?

## docker stop
- graceful shutdown
- safer
- allows cleanup operations

## docker kill
- immediate termination
- force shutdown
- no cleanup opportunity

---

# Q6. Why does terminal get blocked during docker run nginx?

The container runs in foreground mode, attaching container process to the terminal.

Using detached mode avoids terminal blocking:

```bash
docker run -d nginx
```

---

# Q7. Why does container stop after exiting bash shell?

The bash shell is the main process inside the container.

When bash exits, the main process ends, so the container stops.

---

# Q8. Which command is used to enter running container?

```bash
docker exec -it <container-id> bash
```

Used to execute commands inside already running container.

---

# Q9. What happens during docker rm -f?

Docker forcefully stops the running container and removes it immediately.

---

# Q10. Why are docker logs important?

docker logs help identify:
- application failures
- startup issues
- crash reasons
- runtime errors
- debugging information

Very important in Kubernetes and production troubleshooting.

---

# Q11. Does stopped container still exist?

Yes.

Stopped containers remain in the system until removed explicitly.

---

# Q12. Does docker exec create new container?

No.

docker exec only executes commands inside existing running container.

---

# Q13. What runs inside docker run -it ubuntu bash?

The bash shell becomes the main process inside the container.

---

# Q14. Can multiple containers run from same image?

Yes.

Docker images are reusable templates, so multiple containers can be created from the same image.

---

# Q15. Which command both creates and starts a container?

```bash
docker run
```

---

# Q16. Why is docker inspect useful?

docker inspect provides detailed metadata and configuration information such as:
- IP address
- volumes
- environment variables
- networks
- port mappings

Useful for debugging and troubleshooting.

---

# Q17. What happens if main process crashes inside container?

The container stops immediately because container lifecycle depends on the main foreground process.

---

# Q18. Why are logs important in Kubernetes and production?

Logs help identify:
- container crashes
- application errors
- CrashLoopBackOff issues
- startup failures
- runtime issues

Logs are essential for troubleshooting production systems.
