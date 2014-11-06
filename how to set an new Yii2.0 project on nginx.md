# How to set an new Yii2.0 project on nginx Linux

## 設置
* 設置好你的host_config檔 範例:
```
server {
	set $base_path "/home/kettan_wu";
	set $host_path "$base_path/money.yam.com";

	access_log /home/kettan_wu/money.yam.com/log/access.log;
    error_log /home/kettan_wu/money.yam.com/log/error.log;

	server_name money.kettan.com;
	root $host_path/web;
	set $yii_bootstrap "index.php";

	charset utf-8;

	location / {
		#index index.php index.html index.htm;
		index index.html $yii_bootstrap;
		try_files $uri $uri/ /$yii_bootstrap?$args;
	}

	location ~ ^/(protected|framework|themes/\w+/views) {
		deny all;
	}

	#avoid processing of calls to unexisting static files by yii
	location ~ \.(js|css|png|jpg|gif|swf|ico|pdf|mov|fla|zip|rar)$ {
		try_files $uri =404;
	}

	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	location ~ \.php {
		fastcgi_split_path_info ^(.+\.php)(.*)$;

		#let yii catch the calls to unexising PHP files
		set $fsn /$yii_bootstrap;
		if (-f $document_root$fastcgi_script_name) {
			set $fsn $fastcgi_script_name;
		}

		fastcgi_pass 127.0.0.1:9000;
		include fastcgi_params;
		fastcgi_param  SCRIPT_FILENAME  $document_root$fsn;

		#PATH_INFO and PATH_TRANSLATED can be omitted, but RFC 3875 specifies them for CGI
		fastcgi_param  PATH_INFO        $fastcgi_path_info;
		fastcgi_param  PATH_TRANSLATED  $document_root$fsn;
	}

	# prevent nginx from serving dotfiles (.htaccess, .svn, .git, etc.)
	location ~ /\. {
		deny all;
		access_log off;
		log_not_found off;
	}

	#error_page 404 403 http://web.yam.com/
}
```
* 輸入`ln -s /your_config_root/your_config_file /etc/nginx/sites-enabled/your_config_file`把config檔連結到nginx
* 輸入`sudo /etc/init.d/nginx restart`重開伺服器讓設定生效
* 下載一個yii專案壓縮檔.tgz
* `tar zxvf yii-basic-app-2.0.0.tgz`解撒縮project
* 把`assets`, `runtime`, `web/assets`權限設成777
* 把`config/web.php`的`request`改成:
```php
'request' => [
            'enableCsrfValidation' => false,
            'enableCookieValidation' => false,
            'cookieValidationKey' => '',
        ],
```
* enjoy!
