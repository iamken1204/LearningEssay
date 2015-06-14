# AWS

## EC2

### new a ubuntu instance with PHP server
1. Create a instance, checkout the 'free tier' box
2. Donwload the instance's __private key pair__
3. Wait minutes... till the instance is running.
4. Click 'Connect' button
5. `chmod 400 your_private_key.pem`
6. `ssh -i your_private_key.pem ubuntu@your.instance.public.ip`
7. Edit your __Security group__, add `HTTP` port so you can access your web site by public url.
8. [Follow this site's steps](http://blog.winwu.today/2015/05/laravel-on-ubuntu-1404-apache-mysql-php5.html)
   
#### Note
* There is recommend that you install composer into path: `/use/local/bin`   

#### Problem shooting
* I use laravel 5.1 to develop my web app, and I encountered an error message `Failed to open stream Permission denied` when I just set my laravel site up.   
How to solve it?
```shell
$ sudo php artisan cache:clear
$ chmod -R 777 app/storage
```
