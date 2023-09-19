# -*- mode: ruby -*-
# vi: set ft=ruby :

CPU_CORES_COUNT = "1"
MEMORY_COUNT = "1024"

Vagrant.configure("2") do |config|
    config.vm.define "centos" do |centos|
      centos.vm.box = "bento/centos-7"
      centos.vm.network "private_network", ip: "192.168.56.111"
      centos.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.memory = 4096 # Настройка количества памяти для centos
        vb.cpus = 4 # Настройка количества процессоров для centos
      end
    config.vm.synced_folder "./shared", "/shared", type: "virtualbox"
    id_rsa_pub = File.read("#{Dir.home}/.ssh/id_rsa.pub")
    config.vm.provision "copy ssh public key", type: "shell",
    inline: "echo \"#{id_rsa_pub}\" >> /home/vagrant/.ssh/authorized_keys"
  end

  config.vm.define "windows_vpn" do |windows|
    windows.vm.box = "jdesiebenthal/win7"
    windows.vm.network "private_network", ip: "192.168.56.110"
    # windows.vm.communicator = "winrm"
    # windows.winrm.transport = :ssl
    # windows.winrm.ssl_peer_fingerprint = "ac:bd:ef:01:23:45:67:89:ab:cd:ef:01:23:45:67:89:ab:cd:ef"
    # windows.winrm.ssl_ca_cert = "certs/ca_cert.pem"
    # windows.winrm.ssl_cert = "certs/client_cert.pem"
    # windows.winrm.ssl_key = "certs/client_key.pem"
    # windows.winrm.ssl_peer_verification = false
    windows.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.memory = 2048 # Настройка количества памяти для windows_vpn
      vb.cpus = 2 # Настройка количества процессоров для windows_vpn
    end
    config.vm.synced_folder "./shared", "/shared", type: "virtualbox"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sysctl -w net.ipv4.ip_forward=1
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    iptables -A FORWARD -i eth0 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT
    iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
  SHELL
end
