# Pull Ubuntu base image from Docker Hub
docker pull ubuntu

# Run a container named "vps" mapping local port 8000 → container port 80
docker run -it --rm --name=vps -p 8000:80 ubuntu
# -it   = interactive terminal
# --rm  = remove container when stopped
# -p    = publish port mapping
# name  = container name

# Update package lists
apt-get update

# Install essential tools
apt install curl git vim -y
# curl = test web responses
# git  = clone repositories
# vim  = editor

# Go to home directory
cd ~

# Clone your website (replace with real repo)
git clone URL
# Example:
# git clone https://github.com/example/website.git

# Check if nginx is installed
curl localhost:80
# Response: connection refused (because nginx not installed yet)

# Install nginx web server
apt install nginx -y

# Test nginx default response
curl localhost:80
# Should return: HTML of default nginx welcome page

# Check nginx service status
service nginx status

# Start nginx if not running
service nginx start

# Remove default web root files
rm -rf /var/www/html/*
# -r = recursive
# -f = force delete

# Copy website files into nginx web directory
cp -r ins-connections-resource/01-mns-connect-website/* /var/www/html/
# cp -r = copy recursively

# Verify files copied successfully
ls -lah /var/www/html
# Shows list of website files with details

# Test by requesting website through localhost
curl localhost:80
