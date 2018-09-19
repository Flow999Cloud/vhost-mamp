# vhost-mamp


## Edit the following files like sample files

### /etc/hosts
register local server directory
```html
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##

255.255.255.255	broadcasthost
::1             localhost

127.0.0.1	localhost
127.0.0.1   test.test
```

### /Applications/MAMP/conf/apache/httpd.conf

allow access to the httpd-vhosts.conf file
on line 575, remove `#`
```html
# Virtual hosts
Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf
```

allow override `None` to `All` on line 206
```php
<Directory />
    Options Indexes FollowSymLinks
    AllowOverride All
</Directory>
```

### /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf
register localhost first and test local server as following
```php
<VirtualHost *:80>
 ServerName localhost
 DocumentRoot "/Applications/MAMP/htdocs"
</VirtualHost>

<VirtualHost *:80>
 ServerName test.test
 DocumentRoot "/Volumes/my/project/Test"
</VirtualHost>
```


## Update the Apach configuration

Reset the apach port to `80` as attach file(`Mamp configuration.png`)



## Restart Mamp and Enjoy!!!
