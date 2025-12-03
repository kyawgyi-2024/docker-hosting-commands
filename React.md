# React Hosting in Docker (Ubuntu + Nginx)
-------------------------------------------------------

# 1. Pull Ubuntu and run container
docker pull ubuntu
docker run -it --rm --name=vps -p 8000:80 ubuntu

# -it   = interactive terminal
# --rm  = remove container when stopped
# -p    = publish port mapping
# name  = container name


# 2. Update system
apt-get update

# 3. Install sudo
apt install sudo -y

# 4. Install Node.js (v22)
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
apt install nodejs -y

# 5. Check versions
node -v
npm -v

# 6. Install tools (optional)
apt install curl git vim -y

# 7. Clone or copy your react project
cd ~
# git clone <URL>
cd codefile   # enter project folder

# 8. Install dependencies
npm i

# 9. Build production files
npm run build
# output: dist/ (or build/)

# 10. Install nginx
apt install nginx -y

# 11. Start nginx
service nginx start

# 12. Remove default nginx web files
rm -rf /var/www/html/*

# 13. Copy React build files to nginx directory
cp -r dist/* /var/www/html/
# or: cp -r build/* /var/www/html/

# 14. Fix react-router-dom 404 (SPA routing)
vim /etc/nginx/sites-available/default

# Replace this:
# try_files $uri $uri/ =404;

# With this:
try_files $uri /index.html;

# 15. Reload nginx config
nginx -s reload
# explanation:
# -s reload  = reload config without stopping nginx

# 16. Test website
curl localhost:80
# or in browser:
# http://localhost:8000
# or:
# http://SERVER-IP

-------------------------------------------------------
# Dockerfile (optional build method)

FROM node:22 as build
WORKDIR /app
COPY . .
RUN npm i
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

-------------------------------------------------------
# nginx.conf (fix React Router)

server {
    listen 80;
    root /usr/share/nginx/html;

    location / {
        try_files $uri /index.html;
    }
}

# Edit nginx site config
vim /etc/nginx/sites-available/default

# Find this section:
location / {
    try_files $uri $uri/ =404;
}

# Replace with:

location / {
    try_files $uri /index.html;
}


-------------------------------------------------------
