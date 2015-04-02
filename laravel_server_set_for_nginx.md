# Laravel5's server set for Nginx

```
server {

	server_name motc.s2.com;

	access_log /home/kettan_wu/motc.s2.com/host/log/access.log;
	error_log /home/kettan_wu/motc.s2.com/host/log/error.log;

	root /home/kettan_wu/motc.s2.com/www/public;
	index index.php;

	location / {
		index index.php;
		try_files $uri $uri/ /index.php?$query_string;
	}

	location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
