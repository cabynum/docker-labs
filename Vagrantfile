# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.box = "phusion/ubuntu-14.04-amd64"

  #config.vm.hostname = "docker-labs"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.define "node0" do |node0|
    node0.vm.hostname = "node0"
    node0.vm.network "private_network", ip: "192.168.33.10"
    node0.vm.network "public_network", ip: "192.168.33.100", bridge: "en0: Wi-Fi (AirPort)"
    node0.vm.provider "virtualbox" do |vb|
      vb.name = "docker-labs.node0"
      vb.memory = "4096"
      vb.cpus = "2"
    end
  end

  config.vm.define "node1" do |node1|
    node1.vm.hostname = "node1"
    node1.vm.network "private_network", ip: "192.168.33.11"
    node1.vm.network "public_network", ip: "192.168.33.110", bridge: "en0: Wi-Fi (AirPort)"
    node1.vm.provider "virtualbox" do |vb|
      vb.name = "docker-labs.node1"
      vb.memory = "4096"
      vb.cpus = "2"
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.hostname = "node2"
    node2.vm.network "private_network", ip: "192.168.33.12"
    node2.vm.network "public_network", ip: "192.168.33.120", bridge: "en0: Wi-Fi (AirPort)"
    node2.vm.provider "virtualbox" do |vb|
      vb.name = "docker-labs.node2"
      vb.memory = "4096"
      vb.cpus = "2"
    end
  end

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
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
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL

  config.vm.provision "shell", inline: <<-SHELL
    sudo docker 2> /dev/null
    if [ $? -eq 0 ]
      then
        echo "Docker exists, skipping..."
        exit 0
      else
        sudo curl -sSL https://get.docker.com/ | sh
        sudo curl -L https://github.com/docker/compose/releases/download/1.4.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose
        sudo usermod -aG docker vagrant
    fi
    sudo apt-get update
    sudo apt-get install -y tree
    sudo apt-get -y install zsh
    sudo -H -u vagrant bash -c 'git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh'
    sudo curl -L https://raw.githubusercontent.com/cabynum/docker-labs/master/docker-labs.zshrc > /home/vagrant/.zshrc
    sudo chsh -s $(which zsh) vagrant
    sudo -H -u vagrant bash -c 'zsh'
  SHELL
end
