# Docker

## docker installation completed message
```
Quick-Start: Run Boot2Docker (located in Applications), which will open a terminal window. Then, start a test container with: docker run hello-world
•	To save and share container images, automate workflows, and more sign-up for a free Docker Hub account.
•	You can upgrade your existing Boot2Docker VM without data loss by running:  boot2docker upgrade
•	The docker and boot2docker binaries are in /usr/local/bin which you can access from your terminal.  For further information, please see the Docker OS X installation documentation.
```

## docker-machine path
`~/.docker/machine/machines`

## Commands
    $ docker-machine
    $ docker-machine create -drive virtualbox yourMachineName
    $ docker-machine ls
    $ docker-machine env yourMachineName
    $ eval "$(docker-machine env yourMachineName)"
    $ docker images
    $ docker run yourImageName
    
## remove <none> images
[ref](http://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html)
```shell
$ docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

## docker working flow
1. `$ docker-machine start yourVMName`
2. `$ docker pull ubuntu:14.04`
3. `$ docker run -t -i ubuntu:14.04 /bin/bash`

## show containers
to show only running containers
```shell
$ docker ps
```
to show all containers
```shell
$ docker ps -a
```
