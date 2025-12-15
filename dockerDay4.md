# Docker Day-4: Copy File to Container

1. Login to Server
ssh steve@stapp01                               # SSH login to server
# Enter password

2. Prepare File on Host
cd /tmp                                          # Navigate to temporary folder
ls -la                                           # List files in /tmp
cat nautilus.txt.gpg                             # Check file content (encrypted)
(Make sure the file exists and is readable.)

3. Check Running Containers
docker ps                                       # List all running containers
(Identify the container name or ID where the file will be copied (ubuntu_latest in this example).)

4. Access Container (Optional)
docker exec -it ubuntu_latest bash              # Open interactive bash inside container
cd /home                                        # Navigate to home folder inside container
ls -la                                          # Check current files
exit                                            # Exit container
(This step is optional but helps verify destination folder.)

5. Learn Docker cp Command
docker cp --help                                # View usage of docker cp
(docker cp <source_path> <container_name>:<dest_path> copies files/folders from host to container or vice versa.)

6. Copy File to Container
docker cp /tmp/nautilus.gpg ubuntu_latest:/home/    # Copy file into container’s /home
(Copies nautilus.gpg from host /tmp into /home of container ubuntu_latest.)

7. Verify File Inside Container
docker exec -it ubuntu_latest bash             # Re-login into container
cd /home                                        # Go to destination folder
ls -la                                          # Verify file exists
(File should now appear inside the container’s /home directory.)

================================================================================================
# Key Concepts (Interview Ready)

docker ps → Check running containers

docker exec -it <container> bash → Enter interactive shell in container

docker cp <host_path> <container>:<path> → Copy files between host and container

Always verify destination path exists inside container.
================================================================================================
Interview One-Liner:

docker cp allows copying files/folders between host and container; verify inside with docker exec and ls.
====================================================================================================
# Docker Cheat Sheet – DevOps Day Reference

| Command                                    | Purpose / Explanation                                  |
| ------------------------------------------ | ------------------------------------------------------ |
| `docker ps`                                | List running containers (like checking active servers) |
| `docker ps -a`                             | List all containers including stopped ones             |
| `docker images`                            | List all downloaded images on host                     |
| `docker run -it <image> bash`              | Create & run a new container interactively             |
| `docker exec -it <container> bash`         | Enter running container interactively                  |
| `docker stop <container>`                  | Stop a running container gracefully                    |
| `docker start <container>`                 | Start a stopped container                              |
| `docker rm <container>`                    | Remove a stopped container                             |
| `docker rmi <image>`                       | Remove an image from host                              |
| `docker cp <host_path> <container>:<path>` | Copy files from host to container                      |
| `docker logs <container>`                  | View container logs for debugging                      |
| `docker inspect <container>`               | Detailed info about container configuration            |

=================================================================================================
# Key Notes / Tips

1. Interactive mode (-it): Needed to access container shell.

2. File copy (docker cp): Can be host → container or container → host.

3. Container lifecycle: Run → Exec → Stop → Remove.

4. Check before removal: docker ps -a ensures you don’t delete running containers by mistake.

5. Debugging: docker logs is your friend for process troubleshooting.

==============================================================================================
# Interview One-Liners

Docker basics: Containers run isolated apps; docker ps lists them; docker exec opens shell.

File transfer: docker cp moves files between host and container.

Container lifecycle: Run → Stop → Start → Remove → Inspect.
============================================================================================

