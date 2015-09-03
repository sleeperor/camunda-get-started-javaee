# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "box-cutter/ubuntu1404"

  config.vm.network "forwarded_port", guest: 8080, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get dist-upgrade -y
    sudo apt-get install -y htop curl
    curl -sSL https://get.docker.com/ | sh
    sudo usermod -aG docker vagrant
    sudo service docker start
    export DOCKER_COMPOSE_URL=https://github.com/docker/compose/releases/download/1.4.0/docker-compose-`uname -s`-`uname -m`
    sudo su -c "curl -L $DOCKER_COMPOSE_URL > /usr/local/bin/docker-compose"
    sudo su -c "chmod +x /usr/local/bin/docker-compose"
    cd /vagrant && docker-compose up -d
  SHELL
end
