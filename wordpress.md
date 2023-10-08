# Install WordPress on Linode

## Install the LEMP Stack
See the [Linode guide][1]

## Install packages
```
nginx
mariadb-server
php-mysql
php-fpm
```

## Setup MariaDB
```
sudo mysql -u root
```

Create a staging database. Replace `<password>` with a strong password.
```mysql
CREATE DATABASE staging;
CREATE USER 'staging' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON staging.* TO 'staging';
quit
```

Secure your database for production use
```
sudo mysql_secure_installation
```
Answer yes to all of the questions.

## Setup PHP
Edit `/etc/php/8.1/fpm/php.ini`, locate `;cgi.fix_pathinfo=1`, uncomment it and set it to `0`.
```
cgi.fix_pathinfo=0
```

## Setup NGINX
For all following steps, replace `example.com` with your domain.

Create  a root directory for the site
```
sudo mkdir /var/www/html/example.com/public_html
```

Copy the default configuration file for your site
```
sudo cp /etc/nginx/sites-enabled/default /etc/nginx/sites-available/example.com.conf
```

Edit `/etc/nginx/sites-available/example.com.conf`
```nginx
server {
    listen         80;
    listen         [::]:80;
    server_name    example.com www.example.com;
    root           /var/www/html/example.com/public_html;
    index          index.php;

    location / {
      # Send a 404 if the requested page does not exist.
      try_files $uri $uri/ =404;
    }

    # Configure PHP files
    location ~* \.php$ {
      # Specify the socket where PHP listens for incoming connections from other local processes
      fastcgi_pass unix:/run/php/php8.1-fpm.sock;

      # Include variables set in /etc/nginx/fastcgi_params
      include         fastcgi_params;

      # The `fastcgi_param` directives contain the location (relative to the site’s root directory)
      # and file naming convention of PHP scripts to be served when called by NGINX
      fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
      fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
    }
}
```

Create a symlink to your websites configuration in `/etc/nginx/sites-enabled`.
```
ln -s /etc/nginx/sites-available/example.com.conf /etc/nginx/sites-enabled
```

## Enable Firewall
If you enabled UFW on your system, enable the firewall to allow web traffic.
```
sudo ufw app info "Nginx Full"
```
Ports 80 and 443 should be listed as enabled for the `Nginx Full` profile.

If these ports are not allowed, then enable them.
```
sudo ufw allow in "Nginx Full"
```

## Test the LEMP stack

Restart PHP Fast Process Manager
```
sudo systemctl restart php8.1-fpm
```

Reload NGINX
```
sudo nginx -s reload
```
Test your NGINX configuration
```
sudo nginx -t
```

Create a test page to verify NGINX can render PHP and connect to the MariaDB database.
```php
<html>
<head>
    <h2>LEMP Stack Test</h2>
</head>
    <body>
    <?php echo '<p>Hello,</p>';

    // Define PHP variables for the MySQL connection.
    $servername = "localhost";
    $username = "staging";
    $password = "password";

    // Create a MySQL connection.
    $conn = mysqli_connect($servername, $username, $password);

    // Report if the connection fails or is successful.
    if (!$conn) {
        exit('<p>Your connection has failed.<p>' .  mysqli_connect_error());
    }
    echo '<p>You have connected successfully.</p>';
    ?>
</body>
</html>
```

[1]: https://www.linode.com/docs/guides/how-to-install-the-lemp-stack-on-ubuntu-18-04/
