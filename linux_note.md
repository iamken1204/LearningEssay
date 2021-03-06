# Linux Note

### Check hardware name
```shell
dmidecode | grep "Product Name"
```

### Check CPU spec
```shell
cat /proc/cpuinfo | grep name | awk -F: '{print $(NF)}' | uniq -c
```

### View a certain user's processes [ref](http://unix.stackexchange.com/questions/85466/how-to-see-process-created-by-specific-user-in-unix-linux)
```shell
top -U [username]
```

### Clear memory cache
Linux' memory cache manager was located in localhost:11211 by default, use `telnet` to enter it.
```shell
$ telnet localhost 11211
```
After system says ok, insert:
```shell
flush_all
```
then type `quit` to leave talnet mode.

### Empty the contents of a file [ref](http://unix.stackexchange.com/questions/88808/empty-the-contents-of-a-file)
```
$ truncate -s 0 yourFileName
```

### Find which ports are being used now [ref](http://www.cyberciti.biz/faq/what-process-has-open-linux-port/)
* find all   
```shell
$ netstat -tulpn
```
* find a specific port
```shell
$ netstat -tulpn | grep :80
```

### Archive hidden files or directories (dot files)
* Use command below to enable dot file including
```
$ shopt -s dotglob
```
* Use command below to roll back to default setting
```
$ shopt -u dotglob
```
