# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  #config.vm.define  "flunetd setup"
  config.vm.box = "CentOS 6.5 x86_64"
  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.provider :virtualbox do |v, override|
    override.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box"
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end
 
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.define :server do |server_config|
    server_config.vm.network :private_network, ip: "192.168.111.10"
    server_config.vm.hostname = "server"
    server_config.vm "virtualbox" do |vb|
      #   # Don't boot with headless mode
         vb.gui = true
      #
      #   # Use VBoxManage to customize the VM. For example to change memory:
      #   vb.customize ["modifyvm", :id, "--memory", "1024"]
      end
  end
  config.vm.define :agent do |client_config|
    client_config.vm.network :private_network, ip: "192.168.111.12"
    client_config.vm.hostname = "client"
    client_config.vm "virtualbox" do |vb|
      #   # Don't boot with headless mode
         vb.gui = true
      #
      #   # Use VBoxManage to customize the VM. For example to change memory:
      #   vb.customize ["modifyvm", :id, "--memory", "1024"]
      end
     config.vm.provision :ansible do |ansible|
        ansible.inventory_path = "vagrant-inventory.ini"
        ansible.playbook = "site.yml"
        ansible.sudo = "true"
        ansible.sudo_user = "root"
        ansible.host_key_checking = "false"
        ansible.limit = 'all'
      end 
  end
 
 
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder '.', '/vagrant'

  
end
