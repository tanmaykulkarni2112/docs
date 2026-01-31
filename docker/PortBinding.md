# Docker Port Binding

Port binding (or port mapping) in Docker is the process of mapping a port on the host machine to a port inside a running container. This allows you to access an application running inside a container from outside the Docker host.

You can map ports using the `-p` or `--publish` flag when running a container with `docker run`.

## Format

The format for port binding is `HOST_PORT:CONTAINER_PORT`.

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```

- `HOST_PORT`: The port on the host machine.
- `CONTAINER_PORT`: The port inside the container that the application is listening on.

## Example

If you have a web server running on port `80` inside a container, and you want to access it from port `8080` on your host machine, you would run:

```bash
docker run -p 8080:80 my-web-server-image
```

Now, you can access the web server by navigating to `http://localhost:8080` in your web browser.

## Binding to a Specific IP Address

You can also bind to a specific IP address on the host machine:

```bash
docker run -p 192.168.1.100:8080:80 IMAGE_NAME
```

## Publishing All Exposed Ports

The `-P` (uppercase) flag can be used to publish all exposed ports to random ports on the host machine.

```bash
docker run -P IMAGE_NAME
```
You can then use `docker ps` to see which host ports were assigned.