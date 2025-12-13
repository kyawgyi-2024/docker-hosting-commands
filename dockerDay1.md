### Docker Day-1 (Install Docker Packages) — CentOS

ssh banner@ip-hostname                                   # SSH login to remote server
sudo yum update -y                                       # Update all CentOS packages
cat /etc/os-release                                      # Check OS version

sudo yum install -y yum-utils device-mapper-persistent-data lvm2   # Install Docker dependencies
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo   # Add Docker official repo (https://docs.docker.com/engine/install/)

sudo yum install -y docker-ce docker-ce-cli containerd.io          # Install Docker Engine & CLI
docker --version                                         # Check Docker version

sudo systemctl status docker                             # Check Docker service status
sudo systemctl start docker                              # Start Docker service
sudo systemctl status docker                             # Verify Docker is running
sudo systemctl enable docker                             # Enable Docker on boot

sudo yum install -y docker-compose-plugin                # Install Docker Compose v2
docker compose version                                   # Check Docker Compose version


### +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# (Install Docker Packages) — Ubuntu

ssh banner@ip-hostname                                   # SSH login to remote server

sudo apt update                                          # Update package list
sudo apt upgrade -y                                      # Upgrade installed packages
lsb_release -a                                           # Check Ubuntu OS version

sudo apt install -y ca-certificates curl gnupg lsb-release   # Install required packages

sudo mkdir -p /etc/apt/keyrings                          # Create keyrings directory
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg   # Add Docker GPG key

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null   # Add Docker official repo

sudo apt update                                          # Update package list after adding Docker repo
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin   # Install Docker & Compose

docker --version                                         # Check Docker version

sudo systemctl status docker                             # Check Docker service status
sudo systemctl start docker                              # Start Docker service
sudo systemctl enable docker                             # Enable Docker on boot
sudo systemctl status docker                             # Verify Docker is running

docker compose version                                   # Check Docker Compose version


### +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Non-Root Docker User Setup

sudo usermod -aG docker $USER                            # Add current user to docker group
newgrp docker                                            # Apply group change without logout
docker ps                                                # Test Docker without sudo
docker compose version                                   # Check Docker Compose version (v2)


### +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Docker Basics – Interview Q&A

Q1. What is Docker?
→ Docker is a containerization platform to build, ship, and run applications.

Q2. Docker vs Virtual Machine?
→ Docker shares host OS kernel; VM has full OS (Docker is faster & lighter).

Q3. What is a Docker Image?
→ Read-only template used to create containers.

Q4. What is a Docker Container?
→ Running instance of a Docker image.

Q5. What is Dockerfile?
→ A text file with instructions to build a Docker image.

Q6. What is Docker Compose?
→ Tool to run multi-container applications using docker-compose.yml.

Q7. How to check running containers?
→ docker ps

Q8. How to list all containers?
→ docker ps -a

Q9. How to stop a container?
→ docker stop <container_id>

Q10. Why non-root Docker user?
→ Better security and convenience (no sudo needed).

### +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Real Interview Command Tasks (Very Common)

docker images                                      # List all images
docker ps                                          # List running containers
docker ps -a                                       # List all containers

docker pull nginx                                  # Pull image from Docker Hub
docker run -d -p 80:80 nginx                       # Run nginx container
docker stop <container_id>                         # Stop container
docker rm <container_id>                           # Remove container
docker rmi nginx                                   # Remove image

docker logs <container_id>                         # View container logs
docker exec -it <container_id> bash                # Enter running container

docker system df                                   # Check Docker disk usage
docker system prune                                # Clean unused Docker resources

