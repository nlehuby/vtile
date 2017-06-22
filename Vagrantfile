# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/xenial64"

  #config.vm.network :private_network, ip: "192.168.33.10"

  config.vm.synced_folder ".", "/srv"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 1
  end


  config.vm.provision :shell, :privileged => false, :inline => "bash /srv/Vagrant_setup1.sh"
  config.vm.provision :shell, :privileged => false, :inline => "bash /srv/Vagrant_setup2.sh"
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 3579, host: 3579

  config.trigger.before :destroy do
   info "Cleaning up local files..."
   run_remote  "bash /srv/Vagrant_cleanup.sh"
  end
end