# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.hostname = "collectd-berkshelf"
  config.vm.box = "ubuntu-12.04.2-i386-chef-11-omnibus.box"
  config.vm.box_url = "http://grahamc.com/vagrant/ubuntu-12.04.2-i386-chef-11-omnibus.box"
  config.vm.network :private_network, ip: "33.33.33.10"
  config.vm.network :public_network
  config.vm.network :forwarded_port, guest: 80, host: 8085

  # config.vm.synced_folder "../data", "/vagrant_data"

  # config.vm.provider :virtualbox do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  #

  # config.berkshelf.berksfile_path = "./Berksfile"
  config.berkshelf.enabled = true

  # config.berkshelf.only = []
  # config.berkshelf.except = []

  config.vm.provision :chef_solo do |chef|
    chef.json = {
      :instance_role => 'vagrant',
      :collectd => {
        :url => "https://s3.amazonaws.com/collectd-5.4.1/collectd-5.4.1.tar.gz",
        :plugins => {
          :disk => {},
          :load => {},
          :apache => {}
        }
      }
    }

    chef.run_list = [
        "recipe[collectd::default]"
    ]
  end
end
require 'berkshelf/vagrant'
