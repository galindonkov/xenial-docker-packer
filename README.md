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


### How to push the nginx Docker image to Docker hub

- First, you must create an account to the Docker hub and a repository with a name ```nginx64``` : [create docker hub account](https://hub.docker.com/)

- Once you have an account, login with it and create the ```public``` repository : [create a repo](https://www.thegeekdiary.com/how-to-create-a-public-private-repository-in-docker-hub-and-connect-it-remotely-using-command-line/)

- You already have the repo, then go back to the terminal and type : ```docker images```
```vagrant@ubuntu-xenial:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               0.0.1               0af130b61162        About an hour ago   209 MB
```
- Let's create a tag first by : ```docker tag nginx:0.0.1 your-hub-username/nginx64:2018.11.21```

- Check the images again : ```docker images```
```
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
your-hub-user/nginx64   11.21.2018          1727c224629e        24 minutes ago      209 MB
nginx                   0.0.1               1727c224629e        14 minutes ago      209 MB
```
- We are going to upload the fisrt image ```your-hub-user/nginx64```

- Login the the docker hub by : ```docker login``` and use the accunt you previously created once requested.

- Push the image by : ```docker push your-hub-user/nginx64:11.21.2018```

- The image is succesfully uploaded once you see it on the Docker hub as a new tag.
    

### Installation prerequisites needed on the vagrant box - tested on Ubuntu OS

- Install ```ruby-dev , ruby-build``` by : ```apt-get install -y ruby-dev ruby-build```

- Modify you profile and the reload it by : ```echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile``` 
     ```source ~/.bash_profile```
     
- Set up rbenv in your shell by : ```rbenv init```

- Install ruby by : ```rbenv install 2.2.3```

- Select the ruby version for the project by : ```rbenv local 2.2.3```

- Ensure the target version : ```rbenv versions```

- Once you've installed some Ruby versions, you'll want to install gems : ```gem install bundler```

- Install all of the required gems by : ```bundle install```

### Perform kitchen test

- While connected to the vagrant box, go into vagrant directory by : ```cd /vagrant```

- List kitchen environments if any : ```bundle exec kitchen list```

- Build new kitchen environment : ```bundle exec kitchen converge```

- Run the kitchen test by : ```bundle exec kitchen verify```

- After the test passed successfully you ca destroy the created environment by : ```bundle exec kitchen destroy```
