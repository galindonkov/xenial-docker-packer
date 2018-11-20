### Description

Build a Docker Image that has ```nginx``` installed

### Installed softwares needed prior to using the project

- Packer software installation : [link for packer](https://www.packer.io/intro/getting-started/install.html)
- VirtualBox software installation : [link for VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Vagrant software installation : [link for Vagrant](https://www.vagrantup.com/docs/installation/)

### The repo is having following files

- File ```script/provision.sh``` :  a script that installs ```nginx```
- File ```template.json``` : a JSON file that configure the various components of Packer in order to create required machine images
- File ```Gemfile``` : It contains the ruby version and all required by the kitchen bundlers
- File ```.kitchen.yml``` : The kitchen testing configuration file
- File ```test/integration/default/check_pkg.rb``` : a ruby program used by the kitchen to test whether the ```nginx``` is installed


### How to use the repo

#### Note : Below steps have been applied on UbuntuOS, so in order to test it, please follow :

- Clone this repo to your local machines : `git clone git@github.com:galindonkov/packer-nginx64.git`

- Change to the currently added directory : `cd packer-nginx64/`

- Validate the configuration json file by ```packer validate template.json```
  Config file is validated successfully after you get a message : ```Template validated successfully```

- You are ready to build the virtual machine image by : ```packer build template.json```

- The build process is successful once you get a ```nginx64-vbox.box``` placed into your current directory

- Once you have that vbox image the Vagrant program is stepping in to create Vagrant environment by creating an initial Vagrantfile by : ```vagrant init nginx64-vbox.box```

- Created Vagrantfile will be placed into your current directory and right after you can create and configure guest machines according to the Vagrantfile by : ```vagrant up```

- The next step is to ssh into the running Vagrant machine and and get access to its shell by : ```vagrant ssh```
- You should see the command prompt ```vagrant@nginx64:~$``` and then to test whether the ```nginx``` is installed and running by : ```/etc/init.d/nginx status```. The status that proves its running state is : ```Active: active (running)```

- It is good approach to power off or even to destroy the VM if it is not needed further by : ```vagrant halt``` to switch it off and ```vagrant destroy``` to remove it.

#### Additional steps that need to be prepared prior to the kitchen testing

- Installing ```ruby environment``` by : ```brew install rbenv```
- Add ~/.rbenv/bin to your ```$PATH``` for access to the rbenv command-line utility by : ```echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile```
- Reload your profile by : ```source ~/.bash_profile```
- Set up rbenv in your shell by : ```rbenv init```
- Install ```ruby```, recommended version is : ```rbenv install 2.3.1```
- Select the ruby version for the project by : ```rbenv local 2.3.1```
- Ensure the target version : ```rbenv versions```
- Once you've installed some Ruby versions, you'll want to install gems : ```gem install bundler```
- Install all of the required gems by : ```bundle install```

#### After above requirements are met, you can proceed with kitchen tests

- Change to the directory of the cloned repo : ```cd packer-nginx64/```
- List kitchen environments if any : ```bundle exec kitchen list```
- Build new kitchen environment : ```bundle exec kitchen converge```
- Run the kitchen test by : ```bundle exec kitchen verify```
- After the test passed successfully you ca destroy the created environment by : ```bundle exec kitchen destroy```
