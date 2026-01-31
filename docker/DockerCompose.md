# Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services.

Previously, individual containers were created using CLI commands. Docker Compose automates this process by allowing you to define all your services in a single `.yaml` file.

## `docker-compose.yaml` Structure

A `docker-compose.yaml` file contains the configuration for running multiple containers and services. Here is a basic example of its structure:

```yaml
services:
  # A service definition for a container
  my-service:
    image: image_name # Name of the image to use
    ports:
      - "host_port:container_port" # Expose ports
    environment:
      - VAR_NAME=value # Environment variables
    networks:
      - network_name # Networks to attach the container to
```

## Common Commands

To run the services defined in a Docker Compose file, use the following commands:

- To start and run the containers from a specific YAML file in detached mode:
  ```bash
  docker compose -f fileName.yaml up -d
  ```

- To stop and remove the containers, networks, and volumes defined in the YAML file:
  ```bash
  docker compose -f fileName.yaml down
  ```
