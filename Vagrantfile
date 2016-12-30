# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
$script = <<SCRIPT
sudo ifup eth1
sudo yum install -y ntp
sudo systemctl enable ntpd && sudo systemctl start ntpd
sudo cp /home/vagrant/virt7-docker-common-release.repo /etc/yum.repos.d
sudo yum update
sudo yum install -y --enablerepo=virt7-docker-common-release kubernetes docker etcd
sudo systemctl disable firewalld
sudo systemctl stop firewalld

SCRIPT


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  
  config.vm.provision "file", source: "virt7-docker-common-release.repo", destination: "/home/vagrant/virt7-docker-common-release.repo"
  config.vm.provision "shell", inline: $script

  config.vm.provider "virtualbox" do |vb|
    #   # Display the VirtualBox GUI when booting the machine
    #   vb.gui = true
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
 
  config.vm.define "master" do |config|
      config.vm.hostname = "master"
      config.vm.network "private_network", ip: "172.20.20.10", auto_config: false
      config.vm.network "forwarded_port", guest: 8080, host: 8082
  end

  config.vm.define "minion1" do |config|
      config.vm.hostname = "minion1"
      config.vm.network "private_network", ip: "172.20.20.11", auto_config: false
  end

  config.vm.define "minion2" do |config|
      config.vm.hostname = "minion2"
      config.vm.network "private_network", ip: "172.20.20.12", auto_config: false
  end

  config.vm.define "minion3" do |config|
      config.vm.hostname = "minion3"
      config.vm.network "private_network", ip: "172.20.20.13", auto_config: false
  end
end

