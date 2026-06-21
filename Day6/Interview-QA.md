# Day 6 - ENTRYPOINT and CMD Interview Questions & Answers

## Q1. What is the difference between CMD and ENTRYPOINT?

### CMD

Defines the default command executed when a container starts.

Can be overridden using:

```bash
docker run image command
```

### ENTRYPOINT

Defines the main executable that always runs when the container starts.

Remains fixed unless explicitly overridden.

---

## Q2. Which is used for Fixed Executable and Default Arguments?

```text
ENTRYPOINT = Fixed Executable

CMD = Default Arguments
```

Example:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Result:

```bash
python app.py
```

---

## Q3. What happens in:

```Dockerfile
CMD ["echo","Hello"]
```

Run:

```bash
docker run image
```

Output:

```text
Hello
```

Run:

```bash
docker run image ls
```

CMD is replaced by:

```bash
ls
```

---

## Q4. What happens in:

```Dockerfile
ENTRYPOINT ["echo"]
```

Run:

```bash
docker run image Suganya
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

## Q5. What happens when ENTRYPOINT and CMD are used together?

Docker combines them.

Example:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Docker executes:

```bash
python app.py
```

---

## Q6. What happens in:

```bash
docker run image test.py
```

when Dockerfile contains:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Docker executes:

```bash
python test.py
```

CMD is overridden.

ENTRYPOINT remains unchanged.

---

## Q7. A container exits immediately after startup. Which instruction should you check first?

Check:

```Dockerfile
CMD
```

and

```Dockerfile
ENTRYPOINT
```

because container lifecycle depends on the main process.

If the process exits, the container stops.

---

## Q8. Why is this a bad practice?

```Dockerfile
CMD ["apt","install","-y","nginx"]
```

Problems:

* Slow startup
* Internet dependency
* Repeated installation
* Inefficient container execution

Correct approach:

```Dockerfile
RUN apt install -y nginx
```

during image build.

---

## Q9. Can Dockerfile contain multiple RUN, CMD and ENTRYPOINT instructions?

### Multiple RUN

Allowed.

All execute.

---

### Multiple CMD

Allowed.

Only the last CMD is used.

---

### Multiple ENTRYPOINT

Allowed.

Only the last ENTRYPOINT is used.

---

## Q10. Difference between:

```bash
docker run image ls
```

and

```bash
docker run --entrypoint bash image
```

### docker run image ls

Overrides CMD.

---

### docker run --entrypoint bash image

Overrides ENTRYPOINT.

---

# Bonus Question

## Why do production Dockerfiles use ENTRYPOINT + CMD?

Example:

```Dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Benefits:

* Application remains fixed
* Arguments remain flexible
* Easier customization
* Better container design

Run:

```bash
docker run image
```

Result:

```bash
python app.py
```

Run:

```bash
docker run image test.py
```

Result:

```bash
python test.py
```

---

# Frequently Asked One-Liners

### What is CMD?

Default runtime command.

---

### What is ENTRYPOINT?

Main executable.

---

### Can CMD be overridden?

Yes.

---

### Can ENTRYPOINT be overridden?

Yes, using:

```bash
docker run --entrypoint
```

---

### What is the most common production pattern?

```Dockerfile
ENTRYPOINT ["application"]

CMD ["default-arguments"]
```

---

### What happens if the main process exits?

The container stops.

---

### Which instruction is usually fixed?

ENTRYPOINT.

---

### Which instruction is usually flexible?

CMD.

---

### Golden Interview Answer

```text
ENTRYPOINT = Fixed Executable

CMD = Default Arguments
```
