#### Date: 17th November 2025
# Deep Dive into Docker Containers

## 1. What is a Docker Container?
A Docker container is a runnable instance of a Docker image. It is a 
standardized, lightweight, and isolated software unit that packages up code 
and all its dependencies so the application runs quickly and reliably from one 
computing environment to another.

## 2. Container Lifecycle
A container can be in several states:
- **Created:** The container is created but not started.
- **Running:** The container is currently executing its main process.
- **Paused:** The container's processes are suspended.
- **Stopped:** The container's processes are terminated, but the container's 
  state is preserved.
- **Exited:** The container's process has finished (either success or error).
- **Restarting:** The container is being restarted.

## 3. Important Container Commands
- `docker run -d --name <name> -p <host_port>:<container_port> <image>`: Start a 
  container in the background with a name and port mapping.
- `docker exec -it <container_id> /bin/bash`: Execute a command (e.g., shell) 
  inside a running container.
- `docker logs -f <container_id>`: View real-time logs of a container.
- `docker inspect <container_id>`: View detailed information about a container.
- `docker stats`: Display a live stream of container resource usage statistics.
- `docker top <container_id>`: View running processes inside a container.
- `docker pause/unpause <container_id>`: Pause/Resume processes.
- `docker restart <container_id>`: Restart a container.

## 4. Port Mapping and Networking
Containers exist in an isolated network. To access an application running inside 
a container from the host, you must map a port:
- `-p 8080:80`: Maps host port 8080 to container port 80.
- Docker networks (Bridge, Host, None, Overlay) manage how containers 
  communicate with each other and the outside world.

## 5. Environment Variables
You can pass environment variables to a container at runtime:
- `docker run -e MYSQL_ROOT_PASSWORD=password mysql`
- This is crucial for configuring applications dynamically 
  (e.g., database URLs, API keys).

## 6. Resource Constraints
Docker allows you to limit the CPU and Memory a container can use:
- `--memory="512m"`: Limit memory to 512 MB.
- `--cpus="1.5"`: Limit CPU usage to 1.5 cores.
- This prevents a single container from consuming all host resources 
  (Noisy Neighbor problem).

## 7. Cleaning Up
Stopped containers still occupy disk space.
- `docker rm <container_id>`: Remove a specific container.
- `docker container prune`: Remove all stopped containers.
- `docker rm -f $(docker ps -aq)`: Remove all containers (even running ones).

## 8. Best Practices for Containers
- **One Process per Container:** Keep containers focused and simple.
- **Statelessness:** Containers should be ephemeral. Store data in volumes.
- **Small Images:** Use minimal base images (Alpine) to speed up pulls and runs.
- **Security:** Don't run as root inside the container; use a non-privileged 
  user.

## 9. Conclusion
Containers are the executable units of the modern cloud. Understanding their 
lifecycle, management commands, and networking is essential for deploying and 
scaling microservices efficiently across any infrastructure.

---
*End of Notes*
