# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "hashicorp/precise64"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://hashicorp-files.vagrantup.com/precise64.box"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.network :private_network, ip: "192.168.56.110"

  # for mesos web UI.
  config.vm.network :forwarded_port, guest: 5050, host: 5050
  # for Marathon Web UI
  config.vm.network :forwarded_port, guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.name = "vagrant-mesos"
    vb.cpus = 4
    vb.memory = 8*1024
  end

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder '.', '/vagrant'

  config.vm.provision :ansible do |ansible|
    ansible.inventory_path = "vagrant-inventory.ini"
    ansible.playbook = "vagrant-main.yml"
    ansible.extra_vars = { user: "vagrant" }
    ansible.sudo = true
    ansible.limit = 'all'
  end
end
