# Docker Image Layers

A Docker image is not a single, monolithic file. Instead, it is composed of a series of read-only layers. Each layer represents an instruction in the image's Dockerfile.

## Layered Architecture

When you build a Docker image, each command in the Dockerfile creates a new layer. For example:

```Dockerfile
# Base image - creates the first layer
FROM ubuntu:20.04

# Creates a new layer
RUN apt-get update

# Creates another layer
COPY . /app

# And another layer
CMD ["python", "app.py"]
```

Each layer is a set of file system changes. When you run a container from an image, Docker stacks these read-only layers on top of each other.

## The Container Layer

When a container is created from an image, Docker adds a thin, writable layer on top of the read-only image layers. This is often called the "container layer."

- Any changes made inside the running container, such as writing new files, modifying existing files, or deleting files, are written to this writable container layer.
- The underlying image layers remain unchanged.

This architecture has several benefits:

- **Efficiency:** Layers are cached and can be reused across different images, which saves disk space and speeds up image builds.
- **Isolation:** Multiple containers can share the same underlying image layers without interfering with each other, as each container has its own writable layer.
- **Versioning:** When you update an image, only the changed layers need to be downloaded, making updates faster.

## Visualizing Layers

You can think of an image and a container like this:

- **Image:**
  - Read-only Layer 3 (`CMD ["python", "app.py"]`)
  - Read-only Layer 2 (`COPY . /app`)
  - Read-only Layer 1 (`RUN apt-get update`)
  - Base Layer (`FROM ubuntu:20.04`)

- **Container:**
  - Writable Container Layer (where changes are made)
  - Read-only Layer 3
  - Read-only Layer 2
  - Read-only Layer 1
  - Base Layer

When the container is deleted, the writable container layer is also removed, but the underlying image layers persist.
