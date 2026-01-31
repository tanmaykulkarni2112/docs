# Introduction to Docker

This document provides a basic introduction to Docker concepts.

## Why Use Docker?

Docker helps solve common problems in software development and deployment:

- **Dependency Management:** Overcomes the need for manual installation of dependencies.
- **OS Independence:** Ensures that applications run consistently across different operating systems.
- **Consistent Versioning:** Helps maintain consistent versions of libraries and runtimes.

## Core Concepts

### Docker Images and Containers

- **Docker Image:** An executable package that includes everything needed to run an application: the code, a runtime, libraries, environment variables, and configuration files. It's a blueprint for creating a container.
- **Docker Container:** A runnable instance of a Docker image. You can create multiple containers from the same image. A container is a lightweight, standalone, and executable software package.

Think of a Docker image as a "screenshot" of an environment, and a Docker container as a running "instance" of that environment.

### Properties of Docker Containers

1.  **Portable:** Containers can be run on any machine that has Docker installed, regardless of the underlying OS.
2.  **Lightweight:** Containers share the host machine's OS kernel, making them much smaller and faster than virtual machines. You can run multiple containers on a single machine.
3.  **Versionable:** You can create and manage different versions of your application and its environment to facilitate testing and deployment.

## Docker Hub

[Docker Hub](https://hub.docker.com/) is a public registry of Docker images. It's a vast collection of images that you can pull and use to run containers.

When you run a command like `docker run ubuntu`, Docker first checks if you have the `ubuntu` image locally. If not, it will automatically download it from Docker Hub.

```bash
# This command will run an Ubuntu container in interactive mode.
# If the image is not present locally, it will be downloaded from Docker Hub.
docker run -it ubuntu
```

## Docker CLI

The Docker command-line interface (CLI) is the primary tool for interacting with the Docker daemon. The Docker CLI (`docker`) is a client that communicates with the Docker daemon (`dockerd`), which does the heavy lifting of building, running, and managing your containers.