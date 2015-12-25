# Linux and Unix MySQL commands

### open mysql server in osx
`$ mysql.server start`

[reference](http://www.computerhope.com/unix/mysql.htm)

* link to MySQL   
`mysql -h [ip] -u [account] -p[password]`   
__NOTE__ There is no space between `-p`and it's password   

## In MySQL console

* help   
`\h`   

* link to database   
`\r [database's name]`   

* Send command to MySQL   
`[MySQL command]`   
`\G`   

* Show and config mysql's charset [ref](http://stackoverflow.com/questions/3513773/change-mysql-default-character-set-to-utf-8-in-my-cnf)
```
mysql> show variables like "%character%";show variables like "%collation%";
```
You can set mysql's config by specific is variable name, like:
```
mysql> set [Variable_name] = [Value];
```
In order to use traditional chinese in mysql, there is recommended to set collation as utf8_general_ci.
```
mysql> set collation_connection = utf8_general_ci;
mysql> set collation_database = utf8_general_ci;
mysql> set collation_server = utf8_general_ci;
```

## start, stop and restart MySql
[ref](http://coolestguidesontheplanet.com/start-stop-mysql-from-the-command-line-terminal-osx-linux/)
