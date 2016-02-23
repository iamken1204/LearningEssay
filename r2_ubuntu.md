# Creating an nginx_php_mariadb server within Ubuntu 14.04

Ubuntu Server 14.04 LTS (HVM), SSD Volume Type   

## Install and Config

* set server time zone data

```shell
$ dpkg-reconfigure tzdata
```

* create a user

```shell
$ adduser kettan_wu
```

* update apt-get

```shell
$ apg-get update
```

* install nginx

```shell
$ apt-get install nginx
```

* instal php fpm, php mysql, php-cli, php5-mcrypt, php5-curl, php5-imagick, php-gd

```shell
$ apt-get install php5-fpm php5-mysql php5-cli php5-mcrypt php5-curl php5-imagick php5-gd
$ apt-get install php5-memcached memcached
$ php5enmod mcrypt
```

* add or modify  `/etc/nginx/nginx.conf`

```
client_max_body_size 128M;
worker_processes 2; #if instance core is 2
```

* add or modify `/etc/php5/fpm/php.ini`

```
cgi.fix_pathinfo = 0
mbstring.internal_encoding = UTF-8 #unucomment
max_input_vars = 5000
```

* modify `/etc/php5/fpm/pool.d/www.conf`

> for web

```
pm.max_children = 50
pm.start_servers = 10
pm.min_spare_servers = 5
```

> for fps

```
pm.max_children = 100
pm.start_servers = 40
pm.min_spare_servers = 20
pm.max_spare_servers = 60
```

* [Optional] add a EBS to this instance which position at /storage/mysql (only on Dev)

```shell
$ mount /dev/svdf /storage/mysql
```

* install MySQL

```shell
$ apt-get install mariadb-server
```

* set `/etc/mysql/my.cnf` (only on Dev)

```
set datadir = /storage/mysql/data
set default-time-zone = '+8:00'
```

* [Optional] install graph handler imagemagic libaray

```shell
$ apt-get install imagemagick
```


* convert for anyone and it’s orginal path is `/etc/alternatives/convert`


* [Optional] install Fail2ban [@see](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-fail2ban-on-ubuntu-14-04)

```shell
$ apt-get install fail2ban
```

## Install phpMyAdmin

* test mysql
```shell
$ service mysql start
```

* install wget
```shell
$ apt-get install wget
```

* install phpMyAdmin, go to [official site](https://www.phpmyadmin.net/downloads/) and get the download link   
```shell
$ cd /tmp
$ wget https://files.phpmyadmin.net/phpMyAdmin/4.5.5/phpMyAdmin-4.5.5-all-languages.tar.gz
$ tar -xzf phpMyAdmin-4.5.5-all-languages.tar.gz
```
* mv phpmyadmin folder to nginx's default site folder   
```shell
$ mv phpMyAdmin-4.5.5-all-languages phpmyadmin
$ mv ./phpmyadmin /usr/share/nginx/html
```
* modify nginx's default host
```shell
$ vi /etc/nginx/sites-available/default
```
as...
```
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        root /usr/share/nginx/html;
        index index.html index.htm index.php;

        # Make site accessible from http://localhost/
        server_name localhost;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
                # Uncomment to enable naxsi on this location
                # include /etc/nginx/naxsi.rules
        }
        
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
        #       # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
        #
        #       # With php5-cgi alone:
        #       fastcgi_pass 127.0.0.1:9000;
        #       # With php5-fpm:
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        }
}
```
* test link of phpmyadmin
