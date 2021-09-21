# -*- mode: ruby -*-
# vi: set ft=ruby :

QTD_MAQUINAS=2
BOX_PADRAO="ubuntu/focal64"

Vagrant.configure("2") do |config|

  config.vm.box = BOX_PADRAO

  #Maquina Control Panel
  config.vm.define "cpanel" do |vmcp|

    vmcp.vm.network "private_network", ip: "172.28.128.8"

    vmcp.vm.provider "virtualbox" do |vb|
      vb.gui = false
    
      vb.name = "VM_ControlPanel"
      vb.memory = "512"
      vb.cpus = 1
    end 

  vmcp.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y ansible
  SHELL

  end

  (1..QTD_MAQUINAS).each do |n|
  config.vm.define "app#{n}" do |vmapp|

    vmapp.vm.network "private_network", ip: "172.28.128.9#{n}"

    vmapp.vm.provider "virtualbox" do |vb|
      vb.gui = false
    
      vb.name = "VM_Application#{n}"
      vb.memory = "1024"
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
    end

  end

end

end
