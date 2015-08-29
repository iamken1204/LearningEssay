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
    
## remove \<none\> images
[ref](http://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html)
```shell
$ docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```
Another better way: [ref](http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers)
```
$ docker images | grep "<none>" | awk '{print $3}' | xargs docker rmi
```

## docker working flow
1. `$ docker-machine start yourVMName`
2. `$ docker pull ubuntu:14.04`
3. `$ docker run -t -i ubuntu:14.04 /bin/bash`
4. # do somethine in your image
5. `$ docker commit <yourDockerImageID> <username>/<imagename>:<imagetag>` # If you forget image id, you can use `$ docker pa -a` to find it out.

## show containers
to show only running containers
```shell
$ docker ps
```
to show all containers
```shell
$ docker ps -a
```

## remove all containers
[ref (qkrijger's answer is working for me)](http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers)
```
$ docker rm `docker ps --no-trunc -aq`
```

## Mount a host directory as a data volume
[ref](https://docs.docker.com/userguide/dockervolumes/)   
Use `-v` to mount as a data volume.
```
$ docker run -ti -v $PWD/gowiki:/root/go/src/github.com/iamken1204/gowiki kettan/gobuntu:0.0.6 /bin/bash
```

## Link to go web app in docker container
* First we need to find out where is out docker-machine's ip:   
```
$ docker-machine ls
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM
default   *        virtualbox   Running   tcp://192.168.99.100:2376
```
* Then run our container, assign its port `8000` reflect to host's `8000`.
```
$ docker run --rm -ti -p 8000:8000 -v $PWD/gowiki:/root/go/src/github.com/iamken1204/gowiki kettan/gobuntu:0.0.6 /bin/bash
$ cd /root/go/src/github.com/iamken1204/gowiki
$ ./wiki
```
* Finally, we can visit `192.168.99.100:8080` to see our web app!
