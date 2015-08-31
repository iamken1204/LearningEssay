# Docker

## docker-machine path
`~/.docker/machine/machines`

## Commands
    $ docker-machine
    $ docker-machine create -drive virtualbox your-machine-name
    $ docker-machine ls
    $ docker-machine env your-machine-name
    $ eval "$(docker-machine env your-machine-name)"
    $ docker images
    $ docker run your-image-name
    
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
1. `$ docker-machine start your-machine-name`
2. `$ eval "$(docker-machine env your-machine-name)"` \# Eval docker-machine's env so that your OSX can figure out where to find docker.
3. `$ docker pull ubuntu:14.04`
4. `$ docker run -t -i ubuntu:14.04 /bin/bash`
5. # do somethine in your image
6. `$ docker commit <yourDockerImageID> <username>/<imagename>:<imagetag>` # If you forget image id, you can use `$ docker pa -a` to find it out.

## show containers
to show only running containers
```shell
$ docker ps
```
to show all containers
```shell
$ docker ps -a
```
to show all containers' ids
```shell
$ docker ps -aq
```

## remove all containers
[ref (qkrijger's answer is working for me)](http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers)
```
$ docker rm `docker ps --no-trunc -aq`
```

## Mount a host directory as a data volume
[ref](https://docs.docker.com/userguide/dockervolumes/)   
__NOTE__ Currently(docker version _1.8.1_) can only touch files under `/Users` on Mac OSX.
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
