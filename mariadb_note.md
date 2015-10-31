# Mariadb Note

## [Install mariadb by homebrew](https://mariadb.com/blog/installing-mariadb-10010-mac-os-x-homebrew)

## Message of mariadb installed by homebrew
```shell
A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

To connect:
    mysql -uroot

To have launchd start mariadb at login:
  ln -sfv /usr/local/opt/mariadb/*.plist ~/Library/LaunchAgents
Then to load mariadb now:
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist
Or, if you don't want/need launchctl, you can just run:
  mysql.server start
```
