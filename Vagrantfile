# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.

  $etchosts = <<-ETCHOSTS
  echo "192.168.33.100  master" >> /etc/hosts
  echo "192.168.33.101  wnode1" >> /etc/hosts
  echo "192.168.33.102  wnode2" >> /etc/hosts
  echo "192.168.33.103  wnode3" >> /etc/hosts
  ETCHOSTS

  $softinstall = <<-SOFT
  apt-get install -y apt-transport-https ca-certificates curl software-properties-common gnupg2 net-tools
  apt-key add /home/vagrant/docker-key.gpg
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
  apt-get update
  apt-get install -y docker-ce
  apt-key add /home/vagrant/kubernetes-key.gpg
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" >> /etc/apt/sources.list.d/kubernetes.list
  apt-get update
  apt-get install -y kubelet kubeadm kubectl
  apt-mark hold kubelet kubeadm kubectl
  SOFT

  $movedaemon = <<-MOVEDAEMON
  mv /home/vagrant/daemon.json /etc/docker/daemon.json
  MOVEDAEMON

  $swapoff = <<-SWAPOFF
  swapoff -a
  cp /etc/fstab /etc/fstab.orig
  sed -e '/swap/ s/^#*/#/' -i /etc/fstab
  SWAPOFF

  config.vm.define "master" do |master|
    master.vm.box = "debtano/kuberdeb"
    master.vm.box_version = "0.0.1"
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.33.100",
      virtualbox__intnet: true
    master.vm.usable_port_range = 2300..33000
    master.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    master.vm.provision "shell", inline: $etchosts
    master.vm.provision "file", source: "./docker-key.gpg", destination: "docker-key.gpg"
    master.vm.provision "file", source: "./kubernetes-key.gpg", destination: "kubernetes-key.gpg" 
    master.vm.provision "shell", inline: $softinstall
    master.vm.provision "file", source: "./daemon.json", destination: "daemon.json"
    master.vm.provision "shell", inline: $movedaemon
    master.vm.provision "shell", inline: $swapoff
    master.vm.provision "shell", inline: "kubeadm config images pull"
  end

  config.vm.define "wnode1" do |wnode1|
    wnode1.vm.box = "debtano/kuberdeb"
    wnode1.vm.box_version = "0.0.1"
    wnode1.vm.hostname = "wnode1"
    wnode1.vm.network "private_network", ip: "192.168.33.101",
      virtualbox__intnet: true
    wnode1.vm.usable_port_range = 2300..33000
    wnode1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
    wnode1.vm.provision "shell", inline: $etchosts
    wnode1.vm.provision "file", source: "./docker-key.gpg", destination: "docker-key.gpg"
    wnode1.vm.provision "file", source: "./kubernetes-key.gpg", destination: "kubernetes-key.gpg" 
    wnode1.vm.provision "shell", inline: $softinstall
    wnode1.vm.provision "file", source: "./daemon.json", destination: "daemon.json"
    wnode1.vm.provision "shell", inline: $movedaemon
    wnode1.vm.provision "shell", inline: $swapoff
  end
  
  config.vm.define "wnode2" do |wnode2|
    wnode2.vm.box = "debtano/kuberdeb"
    wnode2.vm.box_version = "0.0.1"
    wnode2.vm.hostname = "wnode2"
    wnode2.vm.network "private_network", ip: "192.168.33.102",
      virtualbox__intnet: true
    wnode2.vm.usable_port_range = 2300..33000
    wnode2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
    wnode2.vm.provision "shell", inline: $etchosts
    wnode2.vm.provision "file", source: "./docker-key.gpg", destination: "docker-key.gpg"
    wnode2.vm.provision "file", source: "./kubernetes-key.gpg", destination: "kubernetes-key.gpg" 
    wnode2.vm.provision "shell", inline: $softinstall
    wnode2.vm.provision "file", source: "./daemon.json", destination: "daemon.json"
    wnode2.vm.provision "shell", inline: $movedaemon
    wnode2.vm.provision "shell", inline: $swapoff
  end

  config.vm.define "wnode3" do |wnode3|
    wnode3.vm.box = "debtano/kuberdeb"
    wnode3.vm.box_version = "0.0.1"
    wnode3.vm.hostname = "wnode3"
    wnode3.vm.network "private_network", ip: "192.168.33.103",
      virtualbox__intnet: true
    wnode3.vm.usable_port_range = 2300..33000
    wnode3.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
    wnode3.vm.provision "shell", inline: $etchosts
    wnode3.vm.provision "file", source: "./docker-key.gpg", destination: "docker-key.gpg"
    wnode3.vm.provision "file", source: "./kubernetes-key.gpg", destination: "kubernetes-key.gpg" 
    wnode3.vm.provision "shell", inline: $softinstall
    wnode3.vm.provision "file", source: "./daemon.json", destination: "daemon.json"
    wnode3.vm.provision "shell", inline: $movedaemon
    wnode3.vm.provision "shell", inline: $swapoff
  end
end