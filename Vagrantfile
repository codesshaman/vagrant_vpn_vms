# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.define "machine1" do |machine1|
      machine1.vm.box = "ubuntu/bionic64"
      machine1.vm.network "private_network", ip: "192.168.33.10"
      machine1.vm.provision "shell", inline: "echo 'Hello from Machine 1!'"
    end

    config.vm.define "machine2" do |machine2|
      machine2.vm.box = "ubuntu/bionic64"
      machine2.vm.network "private_network", ip: "192.168.33.11"
      machine2.vm.provision "shell", inline: "echo 'Hello from Machine 2!'"
    end

    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end

    config.vm.provision "shell", inline: <<-SHELL
      sysctl -w net.ipv4.ip_forward=1
      iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
      iptables -A FORWARD -i eth0 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT
      iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
    SHELL
  end
