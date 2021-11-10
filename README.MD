# Devops Intro
## **Life before Devops**
BEFORE DEVOPS, the model used for software development was the “WATERFALL” Model.
The waterfall model is a classical model used in system development life cycle to create a system with a linear and sequential approach.
Disadvantages of waterfall model:
- Makes changes difficult
- Excludes the client and/or end user:
As an internal process, the Waterfall methodology focuses very little on the end user or client involved with a project. Its main purpose has always been to help internal teams move more efficiently through the phases of a project.
- Delays testing until after completion
### **Why Devops**
DevOps is important because it's a software development and operations approach that enables faster development of new products and easier maintenance of existing deployments.
#### **Key Pillars of Devops**
- Easy to use
- Cost effective
- Flexible
- Robust
##### **Monolithic Architecture**
Its where all the code is composed in one piece. E.g. The front end, back end and the databases are written on a single file


### Development Environment
![](images/dev-env.png)
- **DevOps Introduction**
- DevOps is a culture that bridges the gap between Development and Operations
- This is done by creating an environmetn with all the updates and installations necessary to run the application
- The environment can be shared with other employees so that each one of them will have the same VM with the necessary installation requirements
- This overcomes the issue where the application was only working on a certain persons computer
-
- **Life before DevOps**
- Waterfall - V-model
- Transition to Agile methodology and SCRUM framework

- Create `Vagrrantfile` in the current location
```
Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"
# creating a virtual machine ubuntu 

# assign private ip to our VM
 config.vm.network "private_network", ip: "192.168.10.100" 

 # Ensure to install hostsupdater plugin on our localhost before rerunning the vagrantfile
 config.hostsupdater.aliases = ["development.local"]

 # Sync folder from OS to VM
    # "." means current location - into/inside our VM -
 config.vm.synced_folder ".", "/home/vagrant/app"

 # Provide the type of provisioner like "shell, or file" you want to use.
 # If you chose 'file' then you have to provide the source of the file and where
 # you want to save the file on the guest VM.
 # If you chose 'shell' then just provide the path of the script which will run
 # all the installations automatically.
 #config.vm.provision "file", source: "./app/provision.sh", destination: "/home"
 
 config.vm.provision "shell", path: "./app/provision.sh"

end
```
- Create `provision.sh`
```
#!/bin/bash

# Updates system
sudo apt-get update -y

# Upgrades system
sudo apt-get upgrade -y

# Installs nginx server
sudo apt-get install nginx -y

# Opne nginx web server on 192.168.10.100
```
- Commands used today:
```
On the host machine:
- vagrant up (to run the Vagrantfile and create a VM using VB)
- vagrant status (the VM should be running after running vagrant with 'vagrant up')
- type the ip address on the host url bar to see if nginx is working e.g. 
192.168.10.100
- vagrant ssh (to check if the nginx is running which should be if the nginx website opened up)
- vagrant destroy (to destroy the vagrant VM)
- rm -rf .Vagrantfile (after you destroyed the vagrant VM)

try these commands inside of the guest VM:
- systemsctl status nginx (to check the status of the nginx server)
- sudo systemsctl start nginx (starts the nginx server manually)
- sudo systemsctl stop nginx (stops the nginx server manually)
```
- Vagrant commands:
```
Common commands:
     autocomplete    manages autocomplete installation on host
     box             manages boxes: installation, removal, etc.
     cloud           manages everything related to Vagrant Cloud
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     hostsupdater
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     upload          upload to machine via communicator
     validate        validates the Vagrantfile
     version         prints current and latest Vagrant version
     winrm           executes commands on a machine via WinRM
     winrm-config    outputs WinRM configuration to connect to the machine
```
- Testing the Environment to see we have all the necessary packages installed
```
- run 'vagrant up' in /starter-code
- cd into environment/spec-tests
- run these commands here:
gem install bundler
ruby --version
bundle
- next open a new bash terminal and ssh into it
- Run these commands in the VM:
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo apt-get install nodejs -y
sudo apt-get install python-software-properties
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs
sudo npm install pm2 -g
- Next, cd into app/app
- Run these commands:
install npm
npm start
- Run this command on terminal within VS code to see if the necessary packages
- have been installed:
rake spec
- Now you should be able to connect to the website on the port 3000. e.g.:
192.168.10.100:3000
http://192.168.10.100:3000/fibonacci/11
```
### Linux commands
- Who am I `uname` or `uname -a`
- wHERE AM i `pwd` will display currnet location (working directory)
- How can I list contents including hidden files `ls -a`
- Delete file `rm filename` or `rm -rf filename` to forcefully delete
- Create a file `touch filename` or `nano filename`
- Create a directory (folder) `mkdir dir_name`
- Navigate inside directory `cd dir_name`
- List all processes running `ps aux` or `top` inside of the VM
- How too kill a working process `kill process_id/s`
- Wild card is used to deal with multipple files with the same extension `*`
- File permissions `+x executable`
- `read (r) write (w)`
- Check permissions `ll`
- Change premission `chmod permission_required filename`
- `chmod 700` for all `chmod 400` readable
- Print the last 2 lines from a file `tail -2 filename`
- Copy file or folder command in linux?:
- `cp file_path_you_want_2_copy destination_to_copy_the_file_to`
- Cut paste - move file or folder:
- `mv file_path_you_want_2_copy destination_to_copy_the_file_to`
- How to use piping | `ls | head -2`

-**Variable and Environment Variable**
- how to check env var? `env`
- Creating env var `export key=value`
- `export name=mohammed`
- `printenv name`

- Vagranfile for creating multi machines
```
Vagrant.configure("2") do |config|

  # creating a virtual machine ubuntu 
  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/xenial64"

    # assign private ip to our VM
    web.vm.network "private_network", ip: "192.168.10.100"

    # set the host name for your vm
    web.vm.hostname = "web"

    # Sync folder from OS to VM
    web.vm.synced_folder ".", "/home/vagrant/app"

    # provide the provision file to be run for the web app
    web.vm.provision "shell", path: "./environment/provision.sh"
  end

  config.vm.define "mongodb" do |mongodb|

    mongodb.vm.box = "ubuntu/xenial64"
    mongodb.vm.network "private_network", ip: "192.168.10.150"
    mongodb.vm.hostname = "mongodb"
    mongodb.vm.synced_folder ".", "/home/vagrant/app"
    mongodb.vm.provision "shell", path: "./environment/db/provision.sh"
  end
end
```