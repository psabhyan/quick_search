# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "bento/centos-7.2"
  config.vm.hostname = "quicksearch"

  config.ssh.forward_agent = true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.50.21"

  # install git before running ansible provisioner
  config.vm.provision "shell", inline: "yum -y install git"

  # main provisioner
  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_role_file = 'ansible/requirements.yml'
    ansible.playbook = 'ansible/development-playbook.yml'
    ansible.inventory_path = 'ansible/inventories/development.ini'
    ansible.limit = 'all'
  end

  # forward ports
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 3000, host: 7777
  config.vm.network "forwarded_port", guest: 8983, host: 8983

end
