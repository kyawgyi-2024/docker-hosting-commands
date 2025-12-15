# Docker Final Test – DevOps Notes

# Ch-1: Basic Container Run
ssh tony@stapp01                                 # SSH to server
docker ps                                         # List running containers
docker ps -a                                      # List all containers, including stopped
docker run -d --name debug_1 name sleep 1000      # Run container in detached mode with sleep command
docker ps                                         # Verify container is running
(-d = detached mode, sleep 1000 keeps container alive for testing.)

# Ch-2: Running Nginx Container
docker run -d --name nginx_1 nginx:alpine        # Run nginx container in detached mode
docker ps                                        # Verify container is running
(nginx:alpine is lightweight version of Nginx image.)

# Ch-3: Copy Files into Container
cd /tmp
ls -l                                            # Check files in tmp
cd ~
docker ps
docker exec -it <container_id> sh               # Enter container shell
cd /tmp
ls -l
exit                                             # Exit container

docker cp development_3/hello /tmp              # Copy file from host to /tmp
cd /tmp
ls -l                                           # Verify file exists
(docker cp allows host → container file transfer.)

# Ch-4: Copy File into Specific Container Path
docker ps
cd /tmp
docker exec -it ubuntu_latest /bin/bash         # Enter container
cd /usr/src
ls -l
exit

docker exec ubuntu_latest echo $SHELL            # Check default shell (/bin/bash)
docker cp /tmp/hello ubuntu_latest:/usr/src     # Copy file into container path

docker exec -it ubuntu_latest /bin/bash
cd /usr/src
ls -l                                           # Verify file copied
exit
(Useful for placing scripts or data inside container for testing.)

# Ch-5: Docker Images
docker image ls                                  # List images on host
docker pull redis:alpine                         # Pull Redis image
docker pull memcached:alpine                     # Pull Memcached image
docker image ls                                  # Recheck downloaded images
(docker pull fetches image from Docker Hub.)

# Ch-6: Commit Changes to Image
docker ps
docker commit --help                             # Check commit usage
docker commit alpine_nautilus alpine_nautilus    # Save container state as new image
docker ps
docker image ls                                  # Verify new image exists
(docker commit captures container changes into a new image.)

# Ch-7: Create Docker Network
docker network ls                                # List existing networks
docker network create --help                     # Check options
docker network create --driver bridge --subnet <subnet_ip> --gateway <gateway_ip> mysql_network
docker network ls                                # Verify network creation
(Used to connect containers on the same isolated network.)

# Ch-8: Remove Docker Network
docker network ls
docker network rm php-network                   # Remove network
docker network ls                                # Verify removal

# Ch-9: Troubleshoot Containers & Logs
docker ps
docker ps -a
docker logs <container_id>                        # View container logs
docker start <container_id>                       # Start stopped container
docker ps
docker ps -a
docker start <container_id>                       # Ensure container is running
docker ps
docker ps | wc -l                                 # Count number of running containers

(docker logs helps debug application inside container.
docker ps | wc -l → Useful to check how many containers are active (including header line).)

=========================================================================================================
# Key Concepts

Container Lifecycle: run → exec → stop → start → remove.

Images: pull → run → commit → list.

Networking: create → connect → inspect → remove.

File Management: docker cp for host ↔ container transfers.

Debugging: logs, ps, inspect, curl to test apps.
===========================================================================================================

# Interview One-Liners

Containers: Lightweight isolated environments for apps.

Images: Blueprints to create containers.

Networks: Allow communication between containers.

Logs & Exec: Primary tools for container troubleshooting.

File transfer: docker cp moves files between host and container.
===============================================================================================================

# Docker Final Test Cheat Sheet – Interview Ready

| Command                                        | Purpose / Explanation                       |
| ---------------------------------------------- | ------------------------------------------- |
| `docker ps`                                    | List **running containers**                 |
| `docker ps -a`                                 | List **all containers** including stopped   |
| `docker run -d --name <name> <image>`          | Run container in **detached mode**          |
| `docker exec -it <container> bash/sh`          | Enter container shell for testing/debugging |
| `docker cp <host_path> <container>:<path>`     | Copy files **host ↔ container**             |
| `docker start <container>`                     | Start stopped container                     |
| `docker stop <container>`                      | Stop running container                      |
| `docker logs <container>`                      | View container logs for debugging           |
| `docker commit <container> <new_image>`        | Save container changes as new image         |
| `docker pull <image>`                          | Download image from Docker Hub              |
| `docker image ls`                              | List all images on host                     |
| `docker network create --driver bridge <name>` | Create isolated container network           |

==========================================================================================================
# Quick Notes

Container lifecycle: run → exec → start/stop → logs → commit.

Networking: Use bridge or custom networks for multi-container communication.

File transfer: Always verify with ls inside container after docker cp.

Debugging apps: Logs + curl + exec are your first tools.

Image management: pull, commit, and ls help manage versions.
===========================================================================================================

# Interview One-Liner

Docker commands cover container lifecycle, image management, networking, file transfers, and debugging – knowing ps, exec, cp, logs, commit, and network is key.
=================================================================================================================
# Docker Interview Flash Sheet – Super Compact

1. Container Lifecycle

| Command                               | Purpose                               |
| ------------------------------------- | ------------------------------------- |
| `docker run -d --name <name> <image>` | Run container in detached mode        |
| `docker ps`                           | List running containers               |
| `docker ps -a`                        | List all containers including stopped |
| `docker start <container>`            | Start stopped container               |
| `docker stop <container>`             | Stop running container                |
| `docker restart <container>`          | Restart container                     |

2. Access & Debug

| Command                               | Purpose                               |
| ------------------------------------- | ------------------------------------- |
| `docker exec -it <container> bash/sh` | Enter container shell                 |
| `docker logs <container>`             | View logs                             |
| `curl http://localhost:<port>`        | Test application inside container     |
| `docker inspect <container>`          | Check config, ports, network, volumes |

3. Image Management

| Command                                 | Purpose                           |
| --------------------------------------- | --------------------------------- |
| `docker pull <image>`                   | Download image from Docker Hub    |
| `docker image ls`                       | List images                       |
| `docker commit <container> <new_image>` | Save container state as new image |
| `docker rmi <image>`                    | Remove image from host            |

4. File & Volume Management

| Command                                    | Purpose                     |
| ------------------------------------------ | --------------------------- |
| `docker cp <host_path> <container>:<path>` | Copy files host ↔ container |
| `docker volume ls`                         | List volumes                |
| `docker volume create <name>`              | Create volume               |
| `docker volume rm <name>`                  | Remove volume               |

5. Networking

| Command                                        | Purpose                                  |
| ---------------------------------------------- | ---------------------------------------- |
| `docker network ls`                            | List networks                            |
| `docker network create --driver bridge <name>` | Create isolated network                  |
| `docker network inspect <network>`             | Inspect network and connected containers |
| `docker network rm <name>`                     | Remove network                           |


========================================================================================================

Quick Tips / Interview Notes

Container Lifecycle: run → exec → logs → start/stop → commit.

File Transfer: Always verify with ls inside container.

Networking: Bridge network for multi-container communication.

Debugging: Logs + exec + curl are your primary tools.

Images: Pull → Run → Commit → Manage versions.
=================================================================================================
One-Liner Summary

Docker = Containers (run/exec/start/stop) + Images (pull/commit/ls) + Networking (bridge/custom) + Volumes + Debugging (logs/curl) – know these commands for fast DevOps troubleshooting.

==================================================================================================================
