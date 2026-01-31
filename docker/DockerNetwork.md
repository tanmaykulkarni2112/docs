# Docker Networking

When you want containers to communicate with each other, you can create a Docker network and attach the containers to that network. This allows for isolated communication between containers on the same network.

## Docker Network Types (Drivers)

Docker provides different network drivers that suit different use cases. When you create a network, you can specify which driver to use.

### Bridge Network

- **Default network type.** When you start a container without specifying a network, it is attached to a default bridge network.
- Provides IP-based communication between containers on the same host.
- Custom user-defined bridge networks are recommended over the default one for better isolation and manageability.
- **Use case:** Most common scenario where you need multiple containers on the same host to communicate (e.g., a web server and a database).

### Host Network

- **No isolation.** The container shares the network namespace of the host.
- The container's network stack is not isolated from the Docker host. For example, a container running a web server on port 80 will be accessible on port 80 of the host machine.
- **Use case:** When network performance is critical and you don't need network isolation from the host.

### Overlay Network

- Used for **multi-host communication**.
- Allows containers running on different Docker hosts to communicate with each other, which is essential for Docker Swarm services.
- **Use case:** Distributed applications running across multiple nodes in a swarm.

### None Network

- **Disables networking.** The container is not attached to any network and has no network access.
- It has a loopback interface but no external network connectivity.
- **Use case:** For containers that do not need network access, such as batch jobs that only perform file processing.

## Common Network Commands

### List Networks

To get a list of all Docker networks on your system:
```bash
docker network ls
```

### Create a Network

To create a new custom bridge network (the default type):
```bash
docker network create my-bridge-network
```

To specify a different driver, use the `-d` or `--driver` flag:
```bash
docker network create -d host my-host-network
```

### Run a Container on a Network

When you run a container, you can attach it to a specific network:
```bash
docker run -d --network my-bridge-network IMAGE_NAME
```
This is particularly useful when running services that need to communicate, such as a backend application and a database.

**Example with environment variables:**
```bash
docker run -d \
  --network my-bridge-network \
  -e MYSQL_ROOT_PASSWORD=qwerty \
  -e MYSQL_USER=admin \
  mysql
```

### Remove a Network

To remove a Docker network:
```bash
docker network rm NETWORK_NAME
```
**Note:** You cannot remove a network if there are containers still connected to it.

