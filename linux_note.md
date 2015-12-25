# Linux Note

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
