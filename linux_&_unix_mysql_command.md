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

* Show mysql's charset
```
mysql> show variables like "%character%";show variables like "%collation%";
```
In order to use traditional chinese in mysql, there is recommended to set collation as utf8_general_ci.
```
mysql> set collation_connection = utf8_general_ci;
mysql> set collation_connection = utf8_general_ci;
```

## start, stop and restart MySql
[ref](http://coolestguidesontheplanet.com/start-stop-mysql-from-the-command-line-terminal-osx-linux/)
