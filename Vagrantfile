# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
  config.vm.box_version = "3.1.4"
  config.vm.hostname = "centos"
  config.vm.network "private_network", ip: "192.168.211.5"
  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", type: "virtualbox"
  config.vm.provision "shell",
    inline: "dnf install -y python3-pip && pip3 install --user -r /vagrant/requirements.txt"
end
