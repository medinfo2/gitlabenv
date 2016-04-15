# -*- mode: ruby -*-
# vi: set ft=ruby :

# Dotenv.load
ENV['VAGRANT_BRIDGE'] = "Ether"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu14.04"
  if ENV['VAGRANT_BRIDGE']
    interfaces  = %x(VBoxManage list bridgedifs)
    re          = /Name: +(.*#{ENV['VAGRANT_BRIDGE']}.*)/
    if interfaces =~ re
      config.vm.network :public_network, bridge: $1
    end
  else
    config.vm.network "private_network", ip: "192.168.33.10"
  end
  # config.vm.network :public_network, bridge: "en1"
  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.memory = "2048"
    # vb.ioapic = "on"
    vb.cpus = "2"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
    ansible.verbose = 'vvvv'
    ansible.extra_vars = {}
  end
end
