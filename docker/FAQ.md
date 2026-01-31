# Docker Q&A Notes

---

### Question 1: What is the purpose of a Dockerfile?

A Dockerfile defines **how a Docker image is built**. It is a blueprint for creating images, which can then be run as containers.

**Workflow:**
1. Dockerfile → defines steps
2. `docker build` → creates the image
3. `docker run` → starts a container from the image

**Key Point:** Dockerfile builds images; images run as containers.

---

### Question 2: What is a `docker-compose.yaml` file?

A `docker-compose.yaml` file is a configuration file to define and run multiple Docker containers together. It specifies:
- Images or Dockerfiles to use
- Port mappings
- Volumes and file mounts
- Environment variables
- Dependencies and networks

**Key Point:** Dockerfile defines how to build an image; Compose defines how to run containers together.

---

### Question 3: Can a folder contain multiple Dockerfiles?

Yes, a folder can have multiple Dockerfiles with different names (e.g., `Dockerfile.frontend`, `Dockerfile.backend`) or in separate subfolders.

**Usage:**
```bash
docker build -f Dockerfile.frontend -t frontend-image .
```

---

### Question 4: Do we need to build images before using `docker-compose.yaml`?

Not necessarily. If `docker-compose.yaml` has `build:`, Compose will build the image automatically. If it has `image:`, Compose will use the existing image.

---

### Question 5: What does a Dockerfile contain?

A Dockerfile:
- Builds the image (installs dependencies, copies code, sets environment)
- Defines how the container starts via `CMD` or `ENTRYPOINT`

**Key Point:** Dockerfile builds the image and defines the startup command but doesn’t execute the server during the build.

---

### Question 6: How to build a Docker image from a Dockerfile?

```bash
docker build -t image-name .
```

If the Dockerfile has a custom name:
```bash
docker build -f Dockerfile.custom -t custom-image .
```

---

### Question 7: How to run a `docker-compose.yaml` file?

```bash
docker-compose up
```

- Use `-d` to run in detached mode:
```bash
docker-compose up -d
```

---

### Question 8: Example folder structure for `frontend` and `backend` services

```
project-root/
├── docker-compose.yaml
├── frontend/
│   └── Dockerfile
└── backend/
    └── Dockerfile
```

Each service has its own Dockerfile, and `docker-compose.yaml` ties them together.

---

### Question 9: Will `docker-compose.yaml` cause issues with pre-built images?

No. If the service uses `build:`, Compose may rebuild the image (using cache). If it uses `image:`, Compose will reuse the existing image.

---

### Question 10: Should Dockerfiles contain the command to run the code?

Yes. Use `CMD` in Dockerfile for default behavior. Use `command:` in Compose to override it if needed (e.g., for different environments).

---

### Development vs Production Setup

1. **Dockerfile**
   - `Dockerfile.dev`: Development setup (volumes, live reload)
   - `Dockerfile.prod`: Production setup (optimized, smaller image)

2. **docker-compose.yaml**
   - `docker-compose.dev.yaml`: Local testing (mount code, dev environment)
   - `docker-compose.prod.yaml`: Production (pre-built images, no code mounts)

**Commands:**
- Local dev:
  ```bash
  docker-compose -f docker-compose.dev.yaml up
  ```
- Production:
  ```bash
  docker-compose -f docker-compose.prod.yaml up -d
  ```

**Key Point:** Dockerfile defines how to build an image; Compose defines how to run containers. Swap files for dev vs prod environments.

---

### Question 11

**Q:** In the given docker-compose.yaml, there are no `command:` fields for frontend or backend. Does that mean the run commands are in the Dockerfiles?  

**A:**  
Yes.  

- **docker-compose.yaml** only defines:
  - `build:` (where to find Dockerfiles)  
  - `ports:` (host ↔ container mapping)  
  - `networks:` (which network to attach to)  
  - `depends_on:` (startup order)  
  - `healthcheck:` (optional)  

- The **actual run commands** are defined in each service’s **Dockerfile** via `CMD`:  
  - Backend Dockerfile: `CMD ["node", "build/app.js"]`  
  - Frontend Dockerfile: `CMD ["npx", "serve", "dist", "-s"]`  

**Key idea:**  
> `docker-compose up` builds the images (if needed) and runs containers, letting the Dockerfile CMD handle container startup.  
> Compose only overrides CMD if you explicitly provide `command:` in the YAML.

---

### Question 12

**Q:** Is it a common convention to keep run commands in Dockerfiles and not in docker-compose.yaml?  

**A:**  
Yes — this is the **common and recommended convention**.  

**Why:**  
1. **Separation of concerns**  
   - Dockerfile → how to build the image and default run command  
   - docker-compose.yaml → how containers work together (ports, networks, volumes)  

2. **Reusability**  
   - Images can be run directly (`docker run`) or via Compose  
   - Compose just orchestrates multiple containers  

3. **Flexibility**  
   - Compose can override CMD if needed  
   - Keeps Dockerfiles portable for dev, CI/CD, and production  

**Rule of thumb:**  
> Dockerfile contains the “how to run” logic.  
> docker-compose contains the “how to connect and configure multiple services” logic.
