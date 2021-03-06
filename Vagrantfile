# -*- mode: ruby -*-
# vi: set ft=ruby :

# Install basics
BaseBox=<<EOF
  apt-get -y update
  apt-get -y install build-essential libssl-dev
  apt-get -y install epel-release
  apt-get -y install nano byobu bzip2 wget curl git
  timedatectl set-timezone Europe/London
  # Set the right keyboard map
  echo setxkbmap us > /etc/profile.d/setxkbmap.sh
  export TERM=xterm
﻿ export COLORTERM=xfce4-terminal
  export XAUTHORITY=/home/vagrant/.Xauthority
  export DISPLAY=:0.0
  . /etc/profile.d/setxkbmap.sh
EOF

# Install NodeJS v6
Node=<<EOF
  curl -sL https://deb.nodesource.com/setup_6.x | bash -
  apt-get -y install nodejs
EOF

# Install Truffle
Truffle=<<EOF
  npm install -g truffle ethereumjs-testrpc
EOF

# Install Dapple
Truffle=<<EOF
  npm install -g solc dapple
EOF

# Install latest Ethereum dev-kit
Ethereum=<<EOF
  apt-get -y install software-properties-common
  add-apt-repository -y ppa:ethereum/ethereum-qt
  add-apt-repository -y ppa:ethereum/ethereum
  add-apt-repository -y ppa:ethereum/ethereum-dev
  apt-get -y update
  apt-get -y install cpp-ethereum geth
EOF

# Install latest Java JDK
JavaJDK=<<EOF
  if [ ! -f jdk-8u102-linux-x64.rpm ]
  then
    wget --no-cookies --no-check-certificate \
    --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
    http://download.oracle.com/otn-pub/java/jdk/8u102-b14/jdk-8u102-linux-x64.rpm \
    && rpm --install jdk-8u102-linux-x64.rpm
  fi
  JAVA_HOME=/usr/java/jdk1.8.0_102
  JRE_HOME=$JAVA_HOME/jre
  echo export JAVA_HOME=$JAVA_HOME >> /etc/profile.d/java_env.sh
  echo export JRE_HOME=$JRE_HOME >> /etc/profile.d/java_env.sh
EOF

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "acntech/xubuntu"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "https://atlas.hashicorp.com/acntech/boxes/xubuntu/versions/1.0.0/providers/virtualbox.box"

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

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network"

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

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "5120"
  end

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

  # Install Ethereal development environment components
  config.vm.provision "shell", inline: BaseBox
  config.vm.provision "shell", inline: Node
  config.vm.provision "shell", inline: Ethereum
  config.vm.provision "shell", inline: Truffle
  config.vm.provision "shell", inline: Dapple

  config.vm.provision "shell", inline: <<-SHELL
    # Echo the IP configuration
    ifconfig
  SHELL

end
