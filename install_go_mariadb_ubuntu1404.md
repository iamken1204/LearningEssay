# Initial GO & MariaDB in Ubuntu 14.04

1. [Install MariaDB](http://www.liquidweb.com/kb/how-to-install-mariadb-5-5-on-ubuntu-14-04-lts/)
   
2. Install GO [ref1](https://gist.github.com/jniltinho/8758e15a9ef80a189fce) [ref2](http://munchpress.com/install-golang-1-5-on-ubuntu/)
   
   * `$ sudo apt-get update`
     
   * `$ sudo apt-get wget git`
     
   * `$ cd /tmp`
     
   * `$ sudo wget  --no-check-certificate https://storage.googleapis.com/golang/go1.5.2.linux-amd64.tar.gz`
     
   * `$ sudo tar -xzf go1.5.2.linux-amd64.tar.gz`
     
   * `$ mv go /usr/bin/go`
     
   * `$ sudo vi /etc/profile`, Added section of codes below to end of `profile`:
     
     ``` shell
     export PATH=$PATH:/usr/bin/go/bin
     export GOPATH=$HOME/go
     export PATH=$PATH:/$GOPATH/bin
     export GOROOT=/usr/bin/go
     ```
     
   * `$ sudo source /etc/profile` __Important!__ Without this step, the os will forget change of `profile` when you shut it down.
     
   * `$ mkdir $HOME/go ; mkdir $HOME/go/src $HOME/go/pkg $HOME/go/bin`
     
   * Check if the installation was succeeded: `$ go version`