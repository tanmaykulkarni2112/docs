# Docker Command Aliases and Quick Reference

This document provides a quick reference for common Docker commands.

## General Usage

- `sudo`: Use `sudo` before Docker commands if you encounter permission errors.
- `-it`: A combination of `-i` (interactive) and `-t` (pseudo-TTY) flags, used to get an interactive shell into a container.

## Managing Containers

### Listing Containers

- To see all running containers:
  ```bash
  docker ps
  ```

- To see all containers (including stopped ones):
  ```bash
  docker ps -a
  ```

### Running Containers

- To run a container from an image:
  ```bash
  docker run IMAGE_NAME
  ```

- To run a container in interactive mode:
  ```bash
  docker run -it IMAGE_NAME
  ```

- To run a container in detached (background) mode:
  ```bash
  docker run -d IMAGE_NAME
  ```
  **Example:**
  ```bash
  docker run -d -e MYSQL_ROOT_PASSWORD=secret mysql
  ```

- To assign a custom name to a container:
  ```bash
  docker run --name CUSTOM_NAME IMAGE_NAME
  ```

- To map a host port to a container port:
  ```bash
  docker run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
  ```
  **Example:**
  ```bash
  docker run -p 8080:8001 IMAGE_NAME
  ```
  This maps port `8080` on the host to port `8001` in the container.

### Starting and Stopping Containers

- To stop a running container:
  ```bash
  docker stop CONTAINER_NAME_OR_ID
  ```

- To start a stopped container:
  ```bash
  docker start CONTAINER_NAME_OR_ID
  ```

### Removing Containers

- To remove a stopped container:
  ```bash
  docker rm CONTAINER_NAME_OR_ID
  ```
  **Note:** A container must be stopped before it can be removed.

## Managing Images

### Listing Images

- To list all Docker images on your system:
  ```bash
  docker images
  ```

### Pulling Images

- To download an image from a registry (like Docker Hub):
  ```bash
  docker pull IMAGE_NAME
  ```

### Removing Images

- To remove an image:
  ```bash
  docker rmi IMAGE_NAME_OR_ID
  ```
  **Note:** You must remove all containers based on an image before you can remove the image itself.

## Debugging and Execution

### Viewing Logs

- To see the logs of a container:
  ```bash
  docker logs CONTAINER_NAME_OR_ID
  ```

### Executing Commands in a Running Container

- To execute a command inside a running container (e.g., open a shell):
  ```bash
  docker exec -it CONTAINER_NAME_OR_ID /bin/bash
  ```