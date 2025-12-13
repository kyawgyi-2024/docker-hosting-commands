# Docker Day-2 (Nginx on App Server)

ssh user@ip-or-hostname                               # SSH into app server
docker --version                                      # Verify Docker installed
systemctl status docker                               # Check Docker service

docker run -d --name nginx-2 nginx:alpine
docker ps

| Part             | Meaning                      |
| ---------------- | ---------------------------- |
| `docker run`     | Create + start container     |
| `-d`             | Run in background (detached) |
| `--name nginx-2` | Container name               |
| `nginx:alpine`   | Image name                   |

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

docker run -d --name nginx-2 -p 80:80 nginx:alpine    # Run nginx container
docker ps                                             # Verify nginx container is running


### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

systemctl start docker     # Start Docker service
systemctl stop docker      # Stop Docker service
systemctl restart docker   # Restart Docker service
systemctl enable docker    # Start Docker on boot

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

docker run -d --name nginx-2 -p 80:80 nginx:alpine

| Option           | Meaning                           |
| ---------------- | --------------------------------- |
| `docker run`     | Create + start container          |
| `-d`             | Detached mode (run in background) |
| `--name nginx-2` | Custom container name             |
| `-p 80:80`       | Port mapping (host:container)     |
| `nginx:alpine`   | Image name (lightweight nginx)    |

# Port Explanation
-p 80:80 -> Left 80 → server port -> Right 80 → container port

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Docker Basics — Interview Q&A

Q: What is Docker?
A: Docker is a container platform to build, ship, and run applications.

Q: Image vs Container?
A: Image = template, Container = running instance of image.

Q: What is Dockerfile?
A: A file with instructions to build a Docker image.

Q: What is Docker Compose?
A: Tool to manage multi-container apps using docker-compose.yml.

Q: Why containers over VMs?
A: Lightweight, faster startup, less resource usage.

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Real Interview Command Tasks

docker images                                         # List Docker images
docker ps -a                                          # List all containers
docker pull nginx                                     # Download nginx image
docker stop nginx-2                                   # Stop running container
docker rm nginx-2                                     # Remove container
docker rmi nginx                                      # Remove image
docker logs nginx-2                                   # View container logs
docker exec -it nginx-2 sh                            # Access container shell


