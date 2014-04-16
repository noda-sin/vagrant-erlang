# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "CentOS6.4"
  config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130731.box"
  config.vm.network :private_network, ip: "192.168.33.20"

  config.berkshelf.enabled = true

  #config.vm.synced_folder "host_dir", "gest_dir"

  config.vm.provision :chef_solo do |chef|
    chef.run_list = ["erlang"]
  end
end
