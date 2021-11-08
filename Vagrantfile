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
 # If you chose 'file' then you have to provide the source of the file and where you want to save the file on the guest VM
 # If you chose 'shell' then provide the path of the script
 #config.vm.provision "file", source: "./app/provision.sh", destination: "/home"
 config.vm.provision "shell", path: "./app/provision.sh"
 
end
