# Docker Day-3 (Delete Docker Container)

ssh tony@stapp01                                  # SSH login to server
docker --version                                  # Check Docker version
docker ps                                         # List running containers

docker stop kk-container                           # Stop container named 'kk-container'
docker ps                                         # Verify container stopped
docker ps -a                                      # List all containers (running + stopped)

docker rm kk-container                             # Remove container named 'kk-container'
docker ps -a                                      # Verify container removed


### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Docker Run Nginx Container

ssh servername_or_ip_or_hostname                 # SSH login to server
docker --version                                  # Check Docker version
sudo systemctl status docker                      # Check Docker service status

docker run -d --name nginx-2 nginx:alpine        # Run Nginx container in detached mode
docker ps                                        # Verify container is running


### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Docker Day-3 – Interview Q&A & Command Tasks

| Question                                        | Answer / Command                                                                                                      |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| What is Docker?                                 | Docker is a containerization platform that packages applications with their dependencies for consistent environments. |
| Difference between image and container?         | Image: Read-only template; Container: Running instance of an image.                                                   |
| How to check Docker version?                    | `docker --version`                                                                                                    |
| How to list running containers?                 | `docker ps`                                                                                                           |
| How to list all containers (including stopped)? | `docker ps -a`                                                                                                        |
| How to stop a running container?                | `docker stop <container-name-or-id>`                                                                                  |
| How to remove a container?                      | `docker rm <container-name-or-id>`                                                                                    |
| How to remove an image?                         | `docker rmi <image-name-or-id>`                                                                                       |
| How to run a container in detached mode?        | `docker run -d --name <name> <image>`                                                                                 |
| How to view logs of a container?                | `docker logs <container-name-or-id>`                                                                                  |
| How to start a stopped container?               | `docker start <container-name-or-id>`                                                                                 |
| How to restart a container?                     | `docker restart <container-name-or-id>`                                                                               |

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Real Command Tasks (Day-3 Style)

# a) SSH & Verify Docker
ssh tony@stapp01                                # SSH to server
docker --version                                 # Check Docker version
sudo systemctl status docker                     # Verify Docker service

# b) Stop & Remove Containers
docker ps                                        # List running containers
docker stop kk-container                          # Stop container named 'kk-container'
docker ps                                        # Verify container stopped
docker ps -a                                     # List all containers
docker rm kk-container                            # Remove container
docker ps -a                                     # Verify removal

# c) Remove Docker Images
docker images                                    # List all images
docker rmi nginx:alpine                          # Remove specific image
docker images                                    # Verify image removal

# d) Run New Container
docker run -d --name test-container nginx:alpine # Run Nginx container in detached mode
docker ps                                        # Verify container is running
docker logs test-container                        # View container logs

# e) Non-Root User Setup (Optional Task)
sudo usermod -aG docker $USER                    # Add current user to Docker group
newgrp docker                                    # Apply group change without logout
docker ps                                        # Verify non-root Docker access

### ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Tips for Docker Interview Tasks

Always verify Docker service is running: sudo systemctl status docker.

Use docker ps -a to see stopped containers before removal.

Use docker logs <container> to debug container issues.

Non-root Docker usage is preferred in production environments.