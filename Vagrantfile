# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = 2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # vagrantbox
  # https://github.com/CommanderK5/packer-centos-template/releases/download/0.7.1/vagrant-centos-7.1.box
  config.vm.box = "Centos7"

  config.vm.hostname = "LocalEnvironment"
  config.ssh.insert_key = false
  config.ssh.username = "vagrant"

  config.vm.network "private_network", ip: "192.168.33.100"

  config.vm.synced_folder ".", "/vagrant_data"
end