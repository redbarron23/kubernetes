# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<SCRIPT
sudo yum install -y ntp
sudo systemctl enable ntpd && sudo systemctl start ntpd
sudo cp /home/vagrant/virt7-docker-common-release.repo /etc/yum.repos.d
sudo yum update
sudo yum install -y --enablerepo=virt7-docker-common-release kubernets docker

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provision "file", source: "virt7-docker-common-release.repo", destination: "/home/vagrant/virt7-docker-common-release.repo"
  config.vm.provision "shell", inline: $script

  config.vm.define "master" do |master|
      master.vm.hostname = "master"
      master.vm.network "private_network", ip: "172.20.20.10"
  end

  config.vm.define "minion1" do |minion1|
      minion1.vm.hostname = "minion1"
      minion1.vm.network "private_network", ip: "172.20.20.11"
  end

  config.vm.define "minion2" do |minion2|
      minion2.vm.hostname = "minion2"
      minion2.vm.network "private_network", ip: "172.20.20.12"
  end

  config.vm.define "minion3" do |minion3|
      minion3.vm.hostname = "minion2"
      minion3.vm.network "private_network", ip: "172.20.20.13"
  end
end
