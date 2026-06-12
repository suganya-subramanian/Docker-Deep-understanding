# Day 4 - Docker Images and Layers Interview Questions & Answers

## Q1. What is a Docker Image?

A Docker image is a read-only layered template containing application code, runtime, libraries, dependencies, and configuration required to create containers.

---

## Q2. Difference between Docker Image and Docker Container?

### Docker Image

* Read-only template
* Reusable
* Contains application and dependencies

### Docker Container

* Running instance of image
* Contains writable layer
* Executes application processes

---

## Q3. Why are Docker Images read-only?

Docker images are shared by multiple containers.

Making images read-only ensures:

* Consistency
* Reusability
* Isolation
* Predictable behavior

---

## Q4. What are Docker Image Layers?

Docker image layers are reusable filesystem layers stacked together to create a complete image.

Benefits:

* Layer reuse
* Faster builds
* Storage optimization
* Faster downloads

---

## Q5. How does Docker save storage space when multiple images share common layers?

Docker stores common layers only once.

Example:

```text
Image A:
Ubuntu
Python
App-A

Image B:
Ubuntu
Python
App-B
```

Docker stores Ubuntu and Python layers once and only stores application layers separately.

---

## Q6. What is Copy-on-Write?

Copy-on-Write is a mechanism where Docker copies a file from the image layer into the container writable layer before modifying it.

The original image remains unchanged.

---

## Q7. If Container A modifies a file, will Container B see the changes?

No.

Container A stores modifications in its writable layer.

Container B continues using the original image layer.

---

## Q8. What does docker history show?

```bash
docker history nginx
```

Displays:

* Image layers
* Build commands
* Layer sizes
* Layer creation history

---

## Q9. What is an Image ID?

Image ID uniquely identifies image contents.

Images with identical contents can have the same Image ID.

---

## Q10. What does it mean if two images have different names but the same Image ID?

It means both names reference the same underlying image contents.

No duplicate image data exists.

---

## Q11. Does a container modify the Docker image?

No.

Containers modify only their writable layer.

The original image remains unchanged.

---

## Q12. What happens when a container is deleted?

### Image

Remains available.

### Writable Layer

Deleted with the container.

---

## Q13. What is the purpose of image tags?

Tags identify image versions.

Examples:

```text
latest
stable
1.27
dev
```

---

## Q14. Is latest always the newest version?

No.

latest is simply a tag name chosen by the image maintainer.

---

## Q15. Why do DevOps engineers prefer Alpine images?

Advantages:

1. Smaller image size
2. Faster image pull and push
3. Faster deployments
4. Reduced storage usage
5. Smaller attack surface

---

## Q16. A CI/CD pipeline takes 20 minutes to pull a 4.5 GB image. How would you improve it?

Possible solutions:

* Use Alpine base image
* Remove unnecessary packages
* Use multi-stage builds
* Reduce image layers
* Remove build dependencies from final image

---

## Q17. If a container is deleted, will changes made inside it remain?

No.

Changes exist only in the container writable layer.

Deleting the container removes those changes.

---

## Q18. Why are smaller images important in Kubernetes?

Benefits:

* Faster Pod startup
* Faster image pull
* Faster scaling
* Reduced bandwidth usage
* Reduced node storage consumption

---

## Bonus Question

### If 10 Pods use the same image on the same node, will Kubernetes download the image 10 times?

No.

The node downloads the image once.

All Pods reuse the locally cached image layers.

This improves efficiency and reduces bandwidth usage.

---

# Frequently Asked One-Liners

### What is a Docker Image?

Read-only layered template.

---

### What is a Docker Container?

Running instance of an image.

---

### What is Copy-on-Write?

Modify a copied file in writable layer rather than changing image layer.

---

### Why are images read-only?

To ensure consistency and reusability.

---

### What are image layers?

Reusable filesystem layers used to build images.

---

### What is the benefit of layer reuse?

Storage optimization and faster downloads.

---

### What is the writable layer?

The layer where container-specific changes are stored.

---

### Is latest always newest?

No.

It is only a tag name.

---

### Why are Alpine images popular?

Small size and faster deployments.

---

### What happens when a container is deleted?

Writable layer is deleted; image remains.
