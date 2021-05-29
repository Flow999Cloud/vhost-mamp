# Nginx Server Configuration (/etc/nginx/sites-available)

## default

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        # index index.php index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                # try_files $uri $uri/ =404;
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
        }

        include snippets/phpmyadmin.conf;
}
```

## default.laravel

```
server {
    listen 80;
    listen [::]:80;

    root /var/www/html;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name www.yoursite.com;

    #access_log /var/www/html/logs/access.log;
    #error_log /var/www/html/logs/error.log;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

## default.mup

```
upstream meteorapp {
  server 0.0.0.0:<MUP-PORT>;
  keepalive 8;
}

server {
        listen 80;
        listen [::]:80;

        server_name mysite.com;

        location / {
                proxy_pass              http://meteorapp;
                proxy_redirect          off;
                proxy_set_header        Upgrade $http_upgrade;
                proxy_set_header        Connection "upgrade";
        }
}
```

## default.nginx

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
}
```

## default.wordpress

```
server {
    listen 80;
    listen [::]:80;

    root /var/www/html;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name www.yoursite.com;

    #access_log /var/www/html/logs/access.log;
    #error_log /var/www/html/logs/error.log;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location = /favicon.ico { log_not_found off; access_log off; }
    location = /robots.txt { log_not_found off; access_log off; allow all; }
    location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
        expires max;
        log_not_found off;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```


