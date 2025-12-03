# React & TanStack Hosting in Docker (Ubuntu + Nginx)

apt list node                    # check available "node" package
apt list nodejs                  # check available "nodejs" package

apt install sudo -y              # install sudo if missing

curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -

                                 # install NodeSource repo for Node 22

apt install nodejs -y            # install node + npm

node -v                          # verify node version
npm -v                           # verify npm version

cd codefile                      # go into React / TanStack project directory

npm i                            # install dependencies
npm run build                    # create production build

ls                               # verify dist or build exists

# For TanStack, same commands again if needed:
npm i
npm run build
ls -la                           # inspect dist folder

rm -rf /var/www/html/*           # delete default nginx HTML files
cp -r dist/* /var/www/html       # copy production build files

# Same fix as React Router DOM for SPA routing
vim /etc/nginx/sites-available/default

# Change this:
# try_files $uri $uri/ =404;

# To:
try_files $uri /index.html;

nginx -s reload                  # reload nginx config (no restart)
