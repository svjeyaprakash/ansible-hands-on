# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create acs node
  config.vm.define :acs do |acs_config|
      acs_config.vm.box = "ubuntu/trusty64"
      acs_config.vm.hostname = "acs"
      acs_config.vm.network :private_network, ip: "10.0.15.10"
      acs_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
  end

  # create load balancer
  config.vm.define :db do |db_config|
      db_config.vm.box = "centos/7"
      db_config.vm.hostname = "db"
      db_config.vm.network :private_network, ip: "10.0.15.11"
      db_config.vm.network "forwarded_port", guest: 80, host: 8085
      db_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
  end

  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..2).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "10.0.15.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
    end
  end

  # create some app servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..2).each do |i|
    config.vm.define "app#{i}" do |node|
        node.vm.box = "centos/7"
        node.vm.hostname = "app#{i}"
        node.vm.network :private_network, ip: "10.0.15.3#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "809#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
    end
  end

end
