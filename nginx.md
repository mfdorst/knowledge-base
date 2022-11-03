# Nginx static webserver

## Basic assumptions
+ Ubuntu
+ Non-root user with sudo privilege

## Install
```
sudo apt install nginx
```

## Create your website

Static files are served from `/var/www`.

Create a folder within `/var/www` and load your static files into it.

## Set up a virtual host

Edit `/etc/nginx/sites-enabled/default`:
```
server {
    listen 80;
    listen [::]:80;

    # This doesn't matter if you don't actually have a domain
    server_name example.com

    # The directory to search for the index file
    root /var/www/mysite;

    # The name of the index file
    index index.html

    location / {
        # First try to serve files, then directories, then send 404
        try_files $uri $uri =404;
    }
}
```

## Test your nginx configuration
```
sudo nginx -t
```

## Reload nginx
```
sudo service nginx restart
```
