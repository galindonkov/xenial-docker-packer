### Description

Build a Docker Image that has ```nginx``` installed

### Installed softwares needed prior to using the project

- VirtualBox software installation : [link for VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Vagrant software installation : [link for Vagrant](https://www.vagrantup.com/docs/installation/)

### The repo is having following files

- File ```script/provision.sh``` :  a script that installs ```packer``` and ```docker``` on the Vagrant box. 
- File ```template.json``` : a JSON file that configure the various components of Packer in order to create required machine images

### How to use the repo

#### Note : Below steps have been applied on UbuntuOS, so in order to test it, please follow :

- Clone this repo to your local machines : `git clone git@github.com:galindonkov/xenial-docker-packer.git`

- Change to the currently added directory : `cd xenial-docker-packer/`

- Create and configure guest machines according to the Vagrantfile by : ```vagrant up```

- The next step is to ssh into the running Vagrant machine and and get access to its shell by : ```vagrant ssh```
       You should see the command prompt ```vagrant@ubuntu-xenial:~$```
- Make e new directory called ```scripts``` by :  ```mkdir scripts``` and get into it by ```cd scripts/```
    Create a file and open it by ```vi install_nginx.sh```, mark the following text and copy it by ```CTRL+C```
    ```#!/usr/bin/env bash
       #Install curl and nginx
        apt-get update
        apt-get install -y curl
        apt-get install -y nginx
    ```
    Go back to the window with the opened ```install_nginx.sh``` file, type ```a``` and then ```CTRL+V```, then type ```Esc``` key -> ```:wq``` and hit ```Enter```. Go back to the previous directory ```cd ..```
  
 - Create a file ```template.json``` and open it by ```vi template.json``` 



