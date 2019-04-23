# -*- mode: ruby -*-
# vi: set ft=ruby :

NETWORK_BASE = "192.168.2"
NETWORK_NETMASK = "255.255.255.0"
START_SEGMENT = 10

Vagrant.configure(2) do |config|

  config.vm.define :server do |server|
      server.vm.box = "centos/7"
      server.vm.network "public_network", ip: "#{NETWORK_BASE}.#{START_SEGMENT + 1}", netmask: NETWORK_NETMASK
#      server.vm.provision :ansible do |ansible|
#      ansible.playbook = "pmm.yml"
#    end
  end

  config.vm.define :mysql do |mysql|
    mysql.vm.box = "centos/7"
    mysql.vm.network "public_network", ip: "#{NETWORK_BASE}.#{START_SEGMENT + 2}", netmask: NETWORK_NETMASK
#    mysql.vm.provision :ansible do |ansible|
#      ansible.playbook = "node.yml"
#    end
  end
end
