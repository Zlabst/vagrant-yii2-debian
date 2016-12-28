# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

# check and install required Vagrant plugins
required_plugins = ["vagrant-hostmanager", "vagrant-vbguest", "vagrant-cachier"]
required_plugins.each do |plugin|
  if Vagrant.has_plugin?(plugin) then
      #system "echo OK: #{plugin} already installed"
  else
      system "echo Not installed required plugin: #{plugin} ..."
    system "vagrant plugin install #{plugin}"
  end
end

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "debian/jessie64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.22"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder ".", "/vagrant", disabled: false
  #config.vm.synced_folder ".", "/var/www/yii2-app-advanced", owner: "vagrant", group: "vagrant"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  
  config.vm.provider "virtualbox" do |vb|  
    # Display the VirtualBox GUI when booting the machine
    # Don't boot with headless mode
    vb.gui = false
    # Use VBoxManage to customize the VM. For example to change memory:
    #vb.customize ["modifyvm", :id, "--memory", "1024"]
    #vb.customize ["modifyvm", :id, "--name", "LAMP (jessie64)"]
    vb.customize ["modifyvm", :id, "--ostype", "Debian_64"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
    # By default set to 1, change it to amount of your CPUs
    vb.customize ["modifyvm", :id, "--cpus", "2" ]
    # Or uncomment line above for Automatic set VirtualBox guest CPU count to the number of host cores
    # WARNING ! Works on Linux Host ONLY
    # vb.customize ["modifyvm", :id, "--cpus", `grep "^processor" /proc/cpuinfo | wc -l`.chomp ]
    
    # Customize the VM name:
    vb.name = "yii2-adv/jessie64"
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    # Customize the number of vCPUs on the VM:
    vb.cpus = 2
  end
  
  # Set entries in hosts file
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.hostmanager.aliases =  ["yii2.local","admin.yii2.local","phpmyadmin.yii2.local","adminer.yii2.local"]
  
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  
  # Begin Configuring
  config.vm.define "lamp" do|lamp|
    lamp.vm.hostname = "lamp.local" # Setting up hostname

    lamp.vm.provision "shell", inline: "export DEBIAN_FRONTEND=noninteractive"
    lamp.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"
    lamp.vm.provision "shell", inline: "cat ~vagrant/.ssh/me.pub >> ~vagrant/.ssh/authorized_keys"
    lamp.vm.provision "shell", inline: "rm -fr ~vagrant/.ssh/me.pub"
    lamp.vm.provision "shell", inline: "sudo apt-get -y install ansible"
    lamp.vm.provision "shell", inline: "ansible-playbook /vagrant/provisioning/main.yml -i 'vagrant,' --connection=local"
  end
  # End Configuring

end