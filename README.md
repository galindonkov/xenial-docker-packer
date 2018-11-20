### Description

Build a Docker Image that has ```nginx``` installed

### Installed softwares needed prior to using the project

- VirtualBox software installation : [link for VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Vagrant software installation : [link for Vagrant](https://www.vagrantup.com/docs/installation/)

### The repo is having following files

- File ```script/provision.sh``` :  a script that installs ```packer``` and ```docker``` on the Vagrant box. 
- File ```template.json``` : a JSON file that configure the various components of Packer in order to create required machine images
- File ```docker-scripts/install-nginx.sh``` : a script that installs ```curl``` and ```nginx``` on the docker image
- File ```docker.json``` : a JSON file that configure the various components of Packer in order to create required Docker image

### How to use the repo

#### Note : Below steps have been applied on UbuntuOS, so in order to test it, please follow :

- Clone this repo to your local machines : `git clone git@github.com:galindonkov/xenial-docker-packer.git`

- Change to the currently added directory : `cd xenial-docker-packer/`

- Create and configure guest machines according to the Vagrantfile by : ```vagrant up```

- The next step is to ssh into the running Vagrant machine and and get access to its shell by : ```vagrant ssh```
       You should see the command prompt ```vagrant@ubuntu-xenial:~$```

- Change into directory vagrant by ```cd /vagrant```

- Execute ```packer build docker.json``` to get required docker image created.Once the process finished validate the docker image creation by : ```docker images``` and if the output is smillar to following then we have succesfully created a required docker image :

```vagrant@ubuntu-xenial:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               0.0.1               0af130b61162        About an hour ago   209 MB
```


### TO DO

Push nginx Docker image to Docker hub (docker hub)


