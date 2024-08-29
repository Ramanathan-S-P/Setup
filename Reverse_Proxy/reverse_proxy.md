# Reverse Proxy your Existing Server
## Prerequisites
- An Ubuntu server (i.e to be proxied).
- The IP Address of the Server along with TCP Port in which the application is running.
- Domain name pointing to your server's public IP, This will be used in configuring your server using nginx for proxying.
#
## Installing NGINX
refer [NGINX_SETUP](https://github.com/Ramanathan-S-P/Setup/blob/main/Installation/installation.md#nginx)
#
## Configure your Server
All nginx installed servers have a default `.conf` file that displays a `default nginx html page` so rather than altering it create a new `.conf` ( nginx configuration file )
```sh
sudo nano /etc/nginx/sites-available/your_domain.conf
```
make sure you replace `your_domain.conf` with your domain name to avoid ambiguity.<br>
some systems may not have `sites-available` directory so make use of `conf.d` directory.

**`your_domain.conf` need to be configured as given below**
```
server {
    listen 80;
    listen [::]:80;

    server_name your_domain www.your_domain;
        
    location / {
        proxy_pass app_server_address;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        
    }
}

```
This specifies that the nginx listens in `port 80` in your server, so if accessed using `your_domain` or `www.your_domain` via the browser it would be redirected to nginx server which reverse proxies to `app_server_address`,  make sure to replace `server_name` and `app_server_address` with your server_name and app_server_address (i.e where your upstream server or backend server operates so, nginx forwards the requests to the same).

<br>

Refer [hit me!](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-reverse-proxy-on-ubuntu-22-04)  for better understanding how to configure nginx as a reverse proxy server.
<br>

### Create a Symbolic link

**Creating a symbolic link of  `your_domain.conf` present under `/sites-available` to `sites-enabled`** <br>
so that you can down the sites without disturbing their configuration needed and make them live again whenever required.
```sh
sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/
```
### Test the .conf files for syntax errors
```sh
sudo nginx -t
```
### Restart Nginx to run with the applied changes

```sh
sudo systemctl restart nginx
```
**Test your application server using `your_domain` or `www.your_domain` in a browser**

#
## Redirect HTTP Traffic to HTTPS
### Install Certbot
```sh
sudo apt-get install certbot python3-certbot-nginx
```
### Obtain and Install Certificate for `your_domain`
```sh
sudo certbot --nginx
```
This would prompt you for which domains you need SSL Certification else give
<br>

```sh
sudo certbot --nginx -d yourdomain.com
```
replace `yourdomain.com` with your domain name pointing to your app's backend server's public IP.
### Verify `.conf` and restart nginx
```sh
sudo nginx -t
sudo systemctl restart nginx
```