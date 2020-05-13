# docker

> Official documents: [docker docs](https://docs.docker.com/)

## install using the repository

ref: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

### uninstall old versions

``` zsh
sudo apt remove docker docker-engine docker.io containerd runc
```

### set up the repository

1. Update apt package and install packages

``` zsh
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

2. Add Docker's offical GPG key and verify

``` zsh
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

3. Set up the stable repository

``` zsh
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### install docker engine

``` zsh
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### verify docker

``` zsh
$ which docker
/usr/bin/docker
```

## Demo

### RSSHub

[RSSHub docs](https://docs.rsshub.app/)

- download RSSHub image

``` zsh
sudo docker pull diygod/rsshub
```

- run RSSHub

``` zsh
sudo docker run -d --name rsshub -p 1200:1200 diygod/rsshub
```

- stop RSSHub

``` zsh
sudo docker stop rsshub
```

- remove RSSHub

``` zsh
sudo docker stop rsshub
sudo docker rm rsshub
```
