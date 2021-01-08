# -*- mode: ruby -*-
# vi: set ft=ruby :

# README
#
# Getting Started:
# 1. vagrant plugin install vagrant-hostmanager
# 2. vagrant up
# 3. vagrant ssh
#
# This should put you at the control host
#  with access, by name, to other vms
Vagrant.configure(2) do |config|
  config.hostmanager.enabled = true

  config.vm.box = "centos/7"

  config.vm.define "control01", primary: true do |h|
    h.vm.host_name = "control01"
    h.vm.network "private_network", ip: "192.168.135.10"
    h.vm.provision "shell", path: "vagrant/control.sh"
  end

  config.vm.define "sonar01" do |h|
    h.vm.provider :virtualbox do |virtualbox|
      virtualbox.customize ["modifyvm", :id, "--memory", "4096"]
    end

    h.vm.host_name = "sonar01"
    h.vm.network "private_network", ip: "192.168.135.11"
    h.vm.network "forwarded_port", guest: "9000", host: "9000", host_ip: "127.0.0.1"
    h.vm.network "forwarded_port", guest: "5432", host: "5432", host_ip: "127.0.0.1"
    #h.vm.network "forwarded_port", guest: "80", host: "80", host_ip: "127.0.0.1"
    #h.vm.network "forwarded_port", guest: "443", host: "443", host_ip: "127.0.0.1"
    h.vm.provision :shell, path: "vagrant/generic.sh"
  end
end
