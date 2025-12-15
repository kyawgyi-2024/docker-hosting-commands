# Docker Day-5: Troubleshoot Docker Container

1. Login to Server
ssh steve@stapp02                               # SSH login to server
# Enter password

2. Check Running & All Containers
docker ps                                        # List running containers
docker ps -a                                     # List all containers including stopped
(Helps identify container status (running, exited, or paused) and container IDs.)

3. Inspect Container Details
docker inspect <container_id>                    # View detailed info about the container

(Useful to check:
a)Ports mapping (HostPort:ContainerPort)
b)Network settings
c)Environment variables
d)Volume mounts
e)Helps troubleshoot why container might not be accessible.)

4. Test Application Inside Container
curl http://localhost:8080                        # Test if application is responding
(If fails, the container may be stopped or misconfigured.)

5. Start Container if Stopped
docker ps -a                                     # Confirm container status
docker start <container_id>                      # Start the stopped container
docker ps                                        # Verify it is now running
(Ensures container is up and ready to serve traffic.)

6. Re-Test Application
curl http://localhost:8080                        # Check application response again
(Should return application response if container is running correctly.)

================================================================================================================
# Key Concepts (Interview Ready)

docker ps → Check running containers
docker ps -a → Check all containers including stopped
docker inspect → Debug container config & network issues
docker start → Start a stopped container
curl → Test if the app inside container is reachable
=================================================================================================================
Interview One-Liner

Docker troubleshooting involves checking container status with docker ps, inspecting configuration with docker inspect, starting stopped containers, and verifying application response with curl.
==================================================================================================================
# Docker Troubleshooting Cheat Sheet – DevOps Day Reference

| Command                                                  | Purpose / Explanation                                 |
| -------------------------------------------------------- | ----------------------------------------------------- |
| `docker ps`                                              | List all **running containers**                       |
| `docker ps -a`                                           | List **all containers**, including stopped ones       |
| `docker inspect <container_id>`                          | Detailed info: ports, volumes, network, env variables |
| `docker logs <container_id>`                             | View logs to debug application inside container       |
| `docker start <container_id>`                            | Start a stopped container                             |
| `docker stop <container_id>`                             | Stop a running container                              |
| `docker restart <container_id>`                          | Restart container to apply changes                    |
| `docker exec -it <container_id> bash`                    | Enter interactive shell inside container              |
| `docker cp <host_path> <container>:<path>`               | Copy files between host and container                 |
| `curl http://localhost:<port>`                           | Test if application is reachable inside container     |
| `docker rm <container_id>`                               | Remove stopped container                              |
| `docker network ls` / `docker network inspect <network>` | Debug network connectivity issues between containers  |

==============================================================================================================
# Key Notes / Tips

Check container status first: docker ps → running, docker ps -a → all.

Inspect configuration: docker inspect shows ports, IPs, and volumes.

Logs are critical: docker logs is first step in debugging containerized apps.

Connectivity tests: Use curl inside container or from host.

Lifecycle management: Start, stop, restart, or remove containers as needed.

==============================================================================================================
Interview One-Liners

Docker troubleshooting: Check status → inspect → logs → start/restart → test connectivity.

Key commands to memorize: ps, ps -a, inspect, logs, exec, start, curl.
==============================================================================================================

# Docker Networking & Ports Cheat Sheet – DevOps Day Reference

| Command                                              | Purpose / Explanation                                                                  |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `docker ps`                                          | List running containers and mapped ports (`PORTS` column shows host:container mapping) |
| `docker port <container>`                            | Show port mapping of a specific container                                              |
| `docker run -p <host_port>:<container_port> <image>` | Map container port to host port while running container                                |
| `docker inspect <container>`                         | Inspect container network settings, IP, ports, and bridge network                      |
| `docker network ls`                                  | List all Docker networks (bridge, host, none, custom)                                  |
| `docker network inspect <network>`                   | Detailed info about network and connected containers                                   |
| `docker exec -it <container> bash`                   | Enter container shell to test internal connectivity                                    |
| `curl http://localhost:<host_port>`                  | Test container service from host machine                                               |
| `ping <container_ip>`                                | Test connectivity between containers                                                   |
| `docker run --network <network> <image>`             | Connect a container to a specific network                                              |
| `docker network connect <network> <container>`       | Attach running container to a network                                                  |
| `docker network disconnect <network> <container>`    | Detach container from network                                                          |


=============================================================================================================
Key Notes / Tips

Port Mapping: Host:Container format, e.g., 8080:80.

Bridge Network: Default network for container communication.

Custom Networks: Use for multi-container applications for isolation and DNS resolution.

Connectivity Testing: Use curl, ping, or telnet to verify container access.

Network Management: connect / disconnect lets you attach/detach containers from networks dynamically.
===============================================================================================================
# Interview One-Liners

Docker networking basics: Containers use bridge networks by default; host ports are mapped with -p.

Testing connectivity: Use curl, ping, or docker exec to access container services.

Network control: docker network ls/inspect/connect/disconnect manages container connectivity.
=============================================================================================================
