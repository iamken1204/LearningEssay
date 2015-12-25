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
